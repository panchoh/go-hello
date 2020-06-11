# Sign & Go

En este experimento se pretende genertar una implementación de un mecanismo de firma de una release software de manera automatizada.

La firma de una release es un procedimiento que permite generar un elemento (firma digital) que permite identificar unívocamente dicha release y verificar el origen de la misma a todas las personas que quieran usarla.

El problema que surge en la generación de esta firma en los entornos cloud usados para la generación de los artefactos hoy en día es que muchos aspectos quedan fuera de nuestro control con lo que debemos establecer los mecanismos necesarios para garantizar la autenticidad del artefacto generado.

El objetivo es establecer un procedimiento quer permita la generación de una firma de manmera segura y que sea posible detectar cuando se ha generado un artefacto de manera fraudulenta.

Debido a las restricciones de tiempo (limitaciones del CVS y burrocracia, principalmente) se ha implementado un procedimiento con varias carencias y se dan posteriormente otros escenarios que van incrementando progresivamente la seguridasd del proceso.

*El modelo de confianza que se propone es que la release lleva una firma que sólo se puede valizar con una clave publicada en otro repositorio distinto, con lo que es necesario comprometer dos sitios para poder liberar una release fake.*

## Proceso

El proceso general es conocido, usammos una clave privada para generar una firma sobre los artefactos generados de manera que los posteriores usuarios puedan verificar el origen de los mismos. La firma es un fichero que se almacena junto a los artefacos y que son verificables mediante el uso de una clave pública que se almacena en otro lugar.

El principal problema con este proceso es la custodia de la clave provada de firma que tiene que estar accesible desde el motor de CI/CD, esto presenta el riesgo de compromiso de dicha clave.

- Partimos de la existencia de una serie de claves de las personas con potestad de revocar las claves de firma release.
- Tambien tenemos una rama separada en la que se publican las claves públicas de validación.
- El proceso genera un par de claves, la privada se usa para generar la firma y luego se deshecha, la pública se publicará para que los usuarios de los artefactos puedan verificar la firma de los mecanismos.
- A la clave de firma se le añaden los revocadores, estos tienen la capacidad de revocar esta clave en caso de detectarse compromiso.
- Se publica la clave pública en su rama.
- Se generan, firman y publican los artefactos.
- Se deshecha la clave privada.


## Mejoras

### Publicar la clave mediante pull request en el mismo repositorio

Actualmente el proceso se ejecuta en un único pieline que realiza todos los pasos. Esto plantea el problema de que si se comprometen las credenciales Github de un miembro del equipo con permisos se puede generar una versión y una clave.

Una primer posibilidad es la de proteger la rama (nadie puede hacer push) que almacena las claves públicas y requerir de una pull request para añadir modificaciones, esta pull request necesitaría luego de la aprobación por parte de más de un miembro para poderse integrar en dicha rama. De esta manera sería necesaria la intervención de más de un miembro (habría que comprometer más de unas credenciales)

### Publicar la clave mediante pull request en otro repositorio

El escenario anterior se puede violar fácilmente, una subsiguiente mejora sería la de que las claves residieran en otro repositorio distinto (que obviamente tendría otras credenciales). De esta manera habría que comprometer más de unas credenciales, incluso de una persona, para poder publicar una release fake.

### Publicar la clave y el artefacto en distintos repositorios con acceso sólo desde la herramienta de CI/CD

La siguiente mejora es la de restringir los permisos de publicación a la herramienta de CI/CD, con esta separación de responsabilidades se eliminaría la intervancion manual y sería necesario comprometer dos credenciales distintas (una de ellas de servicio)

### Claves firmadas por una entidad de confianza

Por último, para garantizar el origen de los artefactos de la release, sería conveniente que la clave usada para la firma se obtuviera de una fuente de confianza por parte de los consumidores de manera que garantizara el origen de la misma

## PDTE.

Generación de imagen para la construcción y firma que contenga las claves

Usar un action que verifique que las firmas a usar estén reconocidas por el banco

Firmar con clave del banco la clave pública de la release
