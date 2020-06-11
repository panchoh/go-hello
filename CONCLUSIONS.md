# Sign & Go

En este experimento se pretende genertar una implementación de un mecanismo de firma de una release software de manera automatizada.

La firma de una release es un procedimiento que permite generar un elemento (firma digital) que permite identificar unívocamente dicha release y verificar el origen de la misma a todas las personas que quieran usarla.

El problema que surge en la generación de esta firma en los entornos cloud usados para la generación de los artefactos hoy en día es que muchos aspectos quedan fuera de nuestro control con lo que debemos establecer los mecanismos necesarios para garantizar la autenticidad del artefacto generado.

El objetivo es establecer un procedimiento quer permita la generación de una virma de manmera segura y que sea posible detectar cuando se ha generado un artefacto de manera fraudulenta.

Debido a las restricciones de tiempo (limitaciones del CVS y burrocracia, principalmente) se ha implementado un procedimiento con varias carencias y se dan posteriormente otros escenarios que van incrementando progresivamente la seguridasd del proceso.

## Proceso general

El proceso general es conocido, usammos una clave privada para generar una firma sobre los artefactos generados de manera que los posteriores usuarios puedan verificar el origen de los mismos. La firma es un ficher que se almacena junto a los artefacos y que son verificables mediante el uso de una clave pública que se almacena en otro lugar.

El principal problema con este proceso es la custodia de la clave provada de firma que tiene que estar accesible desde el motor de CI/CD, esto presenta el riesgo de compromiso de dicha clave.

- Partimos de la existencia de una serie de claves de las personas con potestad de revocar las claves de firma release.
- El proceso genera un par de claves, la privada se usa para generar la firma y luego se deshecha, la pública se publicará para que los usuarios de los artefactos puedan verificar la firma de los mecanismos
- A la clave de firma se le añaden los revocadores, estos tienen la capacidad de revocar esta clave en caso de detectarse compromiso
- Se publica la clave pública
- Se generan, firman y publican los artefactos
- Se deshecha la clave privada


## Mejoras

### Publicar la clave mediante pull request en el mismo repositorio

### Publicar la clave mediante pull request en otro repositorio

### Publicar la clave y el artefacto en distintos repositorios con acceso sólo desde la herramienta de CI/CD

### Claves firmadas por una entidad de confianza


## PDTE.

Generación de imagen para la construcción y firma que contenga las claves

Usar un action que verifique que las firmas a usar estén reconocidas por el banco

Firmar con clave del banco la clave pública de la release
