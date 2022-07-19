# Amazon Web Services - Simple Storage Service S3

Información compartida [aquí](https://docs.google.com/presentation/d/1ae207ZkDVAuJWqOLAw0KsAo8rn-CM-mHwP4BtZuRuRE/edit?usp=sharing "aquí").

## Características de Amazon S3
- Almacenamiento de objetos (ficheros de cualquier tipo).
- Escalabilidad, disponibilidad de datos, seguridad y gran rendimiento.
- Objetos entre 0 B y 5 TB.
- Almacenamiento ilimitado en el número de objetos.
- Los objetos se almacenan en buckets (directorios/carpetas), cuyos nombres deben ser únicos a nivel global.
- Objeto subido - objeto disponible inmediatamente.
- Si se modifica o elimina un objeto, tardará un tiempo en propagarse los cambios.
- Gestión del ciclo de vida de un objeto (versionamiento).
- Encriptación de objetos.
- Control de acceso por objeto y por bucket.

## S3 - Información de Objetos
- Key: es el nombre del objeto. Usado para recuperar el objeto.
- ID de versión: número de versión del objeto. Generado por Amazon S3 cuando se agrega un objeto a un bucket
- Valor: son los datos del objeto. Puede ser cualquier secuencia de bytes. Desde 0B hasta 5TB.
- Metadatos: información extra sobre el objeto. Conjunto de pares nombre-valor con los que se puede almacenar información relativa al objeto. Amazon S3 asigna metadatos del sistema a estos objetos, pero el usuario también puede definir metadatos a sus objetos.
- Control de acceso: permite especificar quiénes y cómo  pueden utilizar el objeto.
  - Control de acceso basado en recursos.
  - Lista de control de acceso (ACL) o políticas de bucket.
  - Control de acceso basado en usuarios.

## S3 - Tipos de Almacenamiento

### S3 Estándar: 
  99.99% de disponibilidad, 99.99% de durabilidad. Se almacena de forma redundante en múltiples dispositivos y en múltiples instancias.
### S3 IA (Infrequent Access): 
  para datos que no son accedidos de forma frecuente, pero que necesitan un rápido acceso cuando son necesarios. Menor costo que S3 Estándar pero se cobra por acceso al recurso.
### S3 One Zone - IA:
  para datos que se acceden con poca frecuencia y que sólo se almacenarán en una zona geográfica. Menor costo que S3 IA.
### S3 Glacier:
  almacenamiento de menor costo. Se utiliza para archivar datos de larga duración, donde no nos preocupa el tiempo para acceder a los datos (incluso horas).


