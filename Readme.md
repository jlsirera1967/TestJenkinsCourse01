# Readme.md




## 1. Colores (AnsiColor)

* Usamos códigos ANSI como:
  * Azul → `\u001B[34m`
  * Verde → `\u001B[32m`
  * Amarillo → `\u001B[33m`
  * Cian → `\u001B[36m`
  * Rojo → `\u001B[31m`
  * Magenta → `\u001B[35m`
* Reset → `\u001B[0m`


***

## 1. Parallel con fallo

* Jenkins ejecuta las ramas en paralelo.
* **Si una falla (como la rama "Rama con error")**:
  * El stage paralelo se marca como **FAILED**
  * Las otras ramas normalmente continúan hasta terminar
  * El pipeline global se marca como **FAILURE**

***

## 1. Prefijos por rama

Cada rama tiene un prefijo claro:

```
[datos1]
[Datos2]
[datos3]
[ERROR]
```

✔ Esto ayuda a identificar logs cuando están mezclados.

***

## 1. Simulación de carga

```
sleep 5
```

✔ Simula procesamiento pesado en cada rama.

***

## 1. Comportamiento del resumen
* La etapa **Resumen SIEMPRE se ejecuta dentro del flujo**
* Pero el estado final dependerá del fallo

***

## Mejora opcional 

Si quisieras que el pipeline **NO falle aunque una rama falle**, puedes usar:

```groovy
failFast false
```

o capturar el error:

```groovy
catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
    error("Fallo controlado")
}
```

***

