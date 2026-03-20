---
title: 'Implementando un servidor NFS con Docker'
date: 2024-09-29
permalink: /posts/2024/09/servidor-NFS/
tags:
  - Docker
  - Linux
  - Redes TCP/IP
---

**Network File System (NFS)** es un protocolo para sistemas de archivos distribuidos desarrollado por Sun Microsystems en 1984, el cual se basa en el sistema Open Network Computing Remote Procedure Call (ONC RPC).

Se trata de un protocolo que permite a los usuarios cliente acceder y compartir archivos a través de una red de forma similar a cómo se accede de manera local.

NFS funciona por medio de los siguientes tres pasos:

  1. Se verifica que rpc.mountd está instalado y en funcionamiento, este es el demonio que se encarga de escuchar las peticiones de los clientes.
  2. Se crea un directorio en el servidor, el cual representa el punto de enlace entre el servidor y los clientes.
  3. Se configuran permisos en el servidor para permitir la lectura, escritura y ejecución de archivos en el servidor.

Hoy en día, NFS sigue manteniéndose como un protocolo bastante usado principalmente para el manejo de datos centralizados, acceder de forma remota a otro equipo, generar un backup remoto y compartir archivos a través de la red.

## Servidor

Para la realización de este proyecto se utilizo **Ubuntu Server 24.04.4 LTS**.

Comenzamos instalando el paquete de NFS.

```bash
  sudo apt install nfs-kernel-server
```

Creamos un directorio, el cual contendrá los archivos que compartiremos con los clientes.

```bash
  sudo mkdir -p /mnt/nfs-share
```

Modificamos los permisos del directorio para que cualquiera pueda acceder.'

```bash
  sudo chmod -R nobody:nogroup /mnt/nfs-share
  sudo chmod 777 /mnt/nfs-share
```

Accedemos al archivo /etc/exports para añadir el directorio que deseamos compartir.

```bash
  sudo nando /etc/exports 
```

Agregamos la siguiente línea al final del archivo.

```bash
  /mnt/nfs-share 192.168.132.0/24(rw,sync,no_subtree_check,no_root_squash)
```

Colocamos la ruta del directorio, la subred del servidor y, entre paréntesis, algunos parámetros importantes:

* `rw` indica que se pueda leer y escribir los archivos contenidos en el directorio,
* `sync` garantiza que los cambios realizados en el almacenamiento se encuentren estables antes de responder a una petición,
* `no_subtree_check` deshabilita la verificación de seguridad del directorio cuando un cliente montar el directorio y,
* `no_root_squash` permite que cualquier archivo en root sea modificado por un usuario root del sistema cliente.

Para confirmar los cambios realizados al archivo tecleamos el siguiente comando.

```bash
  sudo exportfs -a
```

Ahora, reiniciamos el servicio de NFS.

```bash
  sudo systemctl restart nfs-kernel-server
```

Modificamos la configuración del firewall para que cualquier cliente pueda acceder al servidor.

```bash
  sudo ufw allow from 192.168.132.0/24 to any port nfs
  sudo ufw enable
```

Y verificamos que el puerto correspondiente a NFS este activo.

```bash
  sudo ufw status
```

## Cliente

Del lado del cliente instalamos el paquete correspondiente a NFS, véase que no es el mismo utilizado por el servidor.

```bash
  sudo apt install nfs-common
```

Creamos un directorio, el cual contendrá los archivos del servidor.

```bash
  sudo mkdir -p /mnt/nfs_client
```

Y lo montamos con el siguiente comando, el cual nos pide la IP del servidor, el directorio del servidor y el directorio del cliente.

```bash
  sudo mount 192.168.132.131:/mnt/nfs_share /mnt/nfs_client
```

## Red de contenedores Docker

Comenzamos creando la red con el siguiente comando

```bash
  sudo docker network create --subnet 10.0.1.0/24 --gateway 10.0.1.1 nfs-network
```

Para verificar que se creó la subred utilizamos el siguiente comando.

```bash
  sudo docker network ls
```

Para poder tener acceso al directorio del servidor la lógica que se uso fue, por medio de volúmenes, vincular cada uno de los contenedores al directorio del cliente. De esta forma todos los contenedores tienen un volumen compartido, el cual pueden editar y los cambios se ven reflejados en el servidor.

![Red de contenedores Docker](/images/Blog/ServidorNFS/RedDocker.png)

De tal manera, se configuraron los siguientes contenedores, ambos en la misma red, pero con diferente IP. En el comando se pasa la bandera `--volume` que nos permite vincular un directorio como un volumen compartido para todos los contenedores.

```bash
  sudo docker run -it --ip 10.1.0.10 --network=nfs-network --name nfs_client1 --volume /mnt/nfs_client:/mnt/client1 ubuntu /bin/bash
```

```bash
  sudo docker run -it --ip 10.1.0.20 --network=nfs-network --name nfs_client2 --volume /mnt/nfs_client:/mnt/client2 ubuntu /bin/bash
```
