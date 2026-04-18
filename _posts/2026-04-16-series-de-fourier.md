---
title: 'Series de Fourier'
date: 2026-04-16
permalink: /2026-04/Fourier
tags:
  - Matemáticas
  - Análisis complejo
---

Cualquier señal periódica con frecuencia fundamental $$f_0$$ puede ser aproximada por una suma infinita de senos y cosenos relacionados armónicamente. 

## Señal periódica

Una señal $$x(t)$$ es **periódica** si $$x(t)=x(t+T_0)$$, el menor valor de $$T_0$$ se conoce como periodo fundamental.

## Periodo y frecuencia fundamental

**El periodo** $$T$$ denota el periodo de tiempo en segundos $$[s]$$ en que se repite una señal a partir de un instante de tiempo definido.

**La frecuencia** $$f_0$$ representa la velocidad con la cual la señal vuelve a repetirse, su unidad de medida son los Hertz $$[Hz]$$. Con esto en mente podemos establecer que la frecuencia es el inverso del perido.

$$f_0=\frac{1}{T_0}[Hz]$$

## La serie de Fourier

El matemático Jean-Baptiste Joseph Fourier (1768-1830) se percató de que las funciones pueden ser representadas por sumas de funciones trigonométricas. No entraré en detalle de cómo llegó a dicha conclusión, solo me limitaré a presentar las fórmulas para aproximar una función mediante series de Fourier.

$$x(t)=a_o+\sum_{n=1}^\infty\left\{a_n\cos{\bigg(\frac{2\pi nt}{T_0}\bigg)}+b_n\sin{\bigg(\frac{2\pi nt}{T_0}\bigg)} \right\}$$

Donde,

$$a_0=\frac{1}{T_0}\int_t^{t+T_0}x(t)dt$$

$$a_n=\frac{2}{T_0}\int_t^{t+T_0}x(t)\cos{\bigg(\frac{2\pi nt}{T_0}\bigg)}dt$$

$$b_n=\frac{2}{T_0}\int_t^{t+T_0}x(t)\sin{\bigg(\frac{2\pi nt}{T_0}\bigg)}dt$$

## Armónicos

Las señales pueden representarse en el dominio del tiempo $$x(t)$$ y en el dominio de su frecuencia $$X(f)$$, también denominados como espectro de amplitud $$A$$ y de fase $$\phi$$ respectivamente.

Una señal es **determinista** si es posible definir su valor de amplitud en cualquier instante de tiempo. 

Para cualquier señal determinista, en el dominio de su frecuencia, observamos la presencia de varias **espigas** que se repiten cada cierto tiempo y con una amplitud menor. La primera se denomina **componente fundamental** y el resto de espigas representan sus **componentes armónicas**.

Para una señal $$x(t)$$ definida mediante su serie de Fourier, el término $$a_0$$ representa la componente de DC y los términos senos y cosenos representan las componentes de AC y las componentes armónicas cuando $$n=2$$.

## Teorema de Parseval

La **potencia promedio** $$P$$ de una señal periódica $$x(t)$$ en el dominio de la frecuencia se puede calcular a partir de la suma de las potencias promedio de cada espiga espectral presente en el espectro de amplitud de la señal.

$$P=a_0^2+\frac12\sum_{n=1}^\infty\left\{a_n^2+b_n^2\right\}$$


