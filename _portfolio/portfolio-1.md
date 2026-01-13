---
title: "Pinball 3D"
excerpt: "Proyecto de programación, en el cual se diseñó e implementó un pinball 3D ambientado en el videojuego Hollow Knight<br/><img src='/images/Pinball/pinball3d.jpg'>"
date: 2026-02-08
collection: portfolio
categories:
  - C++
tags:
  - juegos 
---
## Introducción

*OpenGL* (Open Graphic Library) es el API más utilizado en la industria para el desarrollo de aplicaciones gráficas 2D y 3D. Éste opera como un puente entre el software y el hardware de gráficos (GPU).
Entre sus principales características tenemos que:

* Es multiplataforma y multilenguaje.
* Delega los cálculos complejos a la tarjeta de video.
* Emplea un *pipeline* para convertir datos de vértices y texturas en los píxeles que vemos en pantalla.

En este proyecto utilizamos *OpenGL* y C++ para programar un Pinball 3D con temática del videojuego *Hollow Knight*.  

## Estructura del proyecto

El proyecto cuenta con varios archivos y directorios organizados de la siguiente manera:

```text
.
└── Proyecto CGIH02/
    ├── Camera.cpp
    ├── Camera.h
    ├── Window.cpp
    ├── Window.h
    ├── main.cpp
    ├── Models/
    ├── Textures/
    ├── include/
    ├── lib/
    └── shaders/
```

**Camera.h** contiene la clase principal de la cámara, de la cual se obtiene algunos parámetros clave como su posición y ángulo de rotación.

En **Camera.cpp** se capturan las teclas del teclado y la posición del puntero del mouse para determinar en que dirección debe moverse la cámara.

En **Window.h** se declaran los atributos y métodos necesarios para la cámara, las luces, los controles del juego y las animaciones.

**Window.cpp** contiene la clase principal de la ventana que se mostrará en pantalla, así como los métodos que se emplean para capturar las teclas del teclado y los clics del mouse para efectuar diferentes acciones dentro del juego.

Por último, **main.cpp** contiene la función del principal que se ejecutara al iniciar el juego. Dentro de ella se declaró toda la lógica del juego por medio de un ciclo infinito.

## Modelado y ambientación

Todos los modelos fueron creados en Blender. El primero, se modelo a partir de un enemigo del videojuego *Hollow Knight*.

![Enemigo](/images/Pinball/enemigo.png)

Otros modelos fueron más simples de realizar, un huevo y una sierra, los cuales se añadieron como obstáculos y para dar mayor ambientación al escenario.

![Sierra](/images/Pinball/sierra.png)

También se diseñaron dos *skyboxes* para representar el ciclo de día y noche en el escenario, ambas de acuerdo con la temática del pinball.

![Skybox de día](/images/Pinball/dia.png)

Por último, se texturizó el modelo 3D de un gabinete con imágenes relacionadas al juego para adaptarlo a la temática.

![Gabinete](/images/Pinball/gabinete.png)

## Controles

Para el movimiento de los *flippers* se añadieron dos atributos en **Window.h** para obtener el ángulo
de estos, así como sus respectivos *getters*.

En **Window.cpp** se implementaron las teclas X y Z para controlar el ángulo de los *flippers*,
cuando se presiona una tecla el flipper rota 60° y cuando se deja de presionar vuelve
a su estado inicial.

En **main.cpp** al modelo del *flipper* se le asigna el valor del ángulo, mostrando la acción de
movimiento.

Para el resto de objetos se siguió una lógica similar.

## Iluminación

El juego cuenta con varias luces. Una luz direccional se emplea en los *skyboxes*, 4 luces tipo *point light* se emplean en los *flippers* y en los enemigos dispersos por el escenario, y una luz tipo *spot light* se emplea para iluminar desde arriba del tablero.

## Animación básica

La canica del Pinball cuenta con una pequeña animación que muestra como se mueve a traves del escenario. Para ello se emplearon varias variables que funcionaron como banderas de estado y con un bloque *if/else* se determinó la ruta de la canica.

Dentro de los requisitos del proyecto se especificaba crear una animación utilizando *keyframes*, pero por cuestiones de tiempo no se logró implementar.

## Audio

Para los efectos de sonido utilizamos el API de *irrklang*, el cual nos permite agregar audio ambiental, audio 3D y otros sonidos adicionales que hace la experiencia más inmersiva.

## Conclusiones

Este proyecto es el punto de partida para realizar otros proyectos en *OpenGL*, tanto ambientes virtuales 3D como videojuegos, pues en éste se ha logrado implementar tareas como modelado, texturizado, iluminación y animación.

El código posee algunos detalles como valores predefinidos y "números mágicos" que lo hacen difícil de leer, se recomienda encarecidamente revisar el [repositorio](https://github.com/ElliotDM/Proyecto-CGIH02) del proyecto.
