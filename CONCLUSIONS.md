# Sign & Go

En este experimento se pretende genertar una implementación de un mecanismo de firma de una release software de manera automatizada.

La firma de una release es un procedimiento que permite generar un elemento (firma digital) que permite identificar unívocamente dicha release y verificar el origen de la misma a todas las personas que quieran usarla.

El problema que surge en la generación de esta firma en los entornos cloud usados para la generación de los artefactos hoy en día es que muchos aspectos quedan fuera de nuestro control con lo que debemos establecer los mecanismos necesarios para garantizar la autenticidad del artefacto generado.

El objetivo es establecer un procedimiento quer permita la generación de una virma de manmera segura y que sea posible detectar cuando se ha generado un artefacto de manera fraudulenta.

Debido a las restricciones de tiempo (limitaciones del CVS y burrocracia, principalmente) se ha implementado un procedimiento con varias carencias y se dan posteriormente otros escenarios que van incrementando progresivamente la seguridasd del proceso.

## Proceso general



## Mejoras

### Publicar la clave mediante pull request en el mismo repositorio

### Publicar la clave mediante pull request en otro repositorio

### Publicar la clave y el artefacto en distintos repositorios con acceso sólo desde la herramienta de CI/CD



## PDTE.

Generación de imágen para la construcción y firma que contenga las claves

Usar un action que verifique que las firmas a usar estén reconocidas por el banco

Firmar con clave del banco la clave pública de la release
