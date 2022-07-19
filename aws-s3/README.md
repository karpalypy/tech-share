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

## S3 - Esquema de costos
- Por almacenaje de objetos.
- Por peticiones de acceso (S3 IA, S3 Zone IA y S3 Glacier).
- Por transferencia de datos entre regiones (replicación de datos).
- Por transferencia acelerada.
S3 permite gestionar precios por cada objeto por separado, haciendo uso de etiquetas que permiten desglosar los gastos.

## S3 - Bucket con control de versiones
- Habilitar el control de versiones en las propiedades del Bucket.
- Se versiona un objeto, cuando se sobreescribe. Siempre se puede restaurar a la versión anterior.
- ¿Costo? Se aplican tasas normales por cada versión del objeto almacenado y transferido ( cada versión del objeto es un objeto en sí).
- Si se habilita el control de versiones en un bucket por primera vez, es posible que el cambio se propague por completo en un instante. Para emitir operaciones de escritura (PUT o DELETE) en los objetos del bucket, se recomienda que espere 15 minutos después de habilitar el control de versiones.

## S3 - Bucket para replicación de objetos (Backup)
- Crear un **bucket destino** en otra zona geográfica (es lo normal en un backup, para guardarlo en otro datacenter).
- Habilitar el control de versiones en el bucket destino.
- Crear **regla de replicación** en el **bucket origen**, indicando el **bucket destino** (backup). Incluso podemos usar un bucket de otra cuenta de AWS.

## S3 - Ciclo de vida de los objetos de un bucket
Nos permite administrar los objetos de manera que se almacenen de manera económica durante todo su ciclo de vida.
Existen dos tipos de acciones: 
- **Acciones de transición**: definen el momento en que los objetos pasan a otra clase de almacenamiento (S3 Estándar a S3 Glacier).
- **Acciones de vencimiento**: definen el momento en que vencen los objetos. Amazon S3 elimina automáticamente los objetos que han vencido.
Estas configuraciones están en el tab de Administración del bucket.

## S3 - Seguridad y Encriptación

- Todos los buckets de S3 por defecto son privados.
- Se puede cambiar la configuración de control de acceso mediante:
  - Listas de control de acceso ACL.
  - Políticas del bucket.
- Los buckets pueden ser configurados para crear logs de acceso de todas las peticiones que se realicen sobre el bucket, y ser almacenados en otro bucket de respaldo.

- Encriptación en los datos en tránsito:
  - SSL / TLS.
- Encriptación en el lado del servidor:
  - SSE-S3: claves gestionadas.
  - SSE-KMS: servicio de gestión de claves.
  - SSE-C: encriptación en el servidor con las claves del cliente.
- Encriptación en el lado del cliente.

## S3 - Transfer Acceleration
La aceleración de transferencia de datos es un propiedad de bucket que permite transferir archivos de manera rápida, fácil y segura entre un cliente y un bucket de S3 a larga distancia.
**Transfer Accelerate** aprovecha las ubicaciones de borde, las más cercanas al cliente y distribuidas globalmente de Amazon CloudFront para redirigir los datos a Amazon S3 a través de una ruta de red optimizada.

<p align="center"><b>
nombredelbucket.s3-accelerate.amazonaws.com</p></b>
<p style='text-align: center;'>

¿Cuando usarlo? 
- Clientes que cargan a un bucket centralizado desde todo el mundo.
- Transferencia de gran volumen de datos regularmente entre varios continentes.

## Diferencias entre Amazon S3 y Amazon CloudFront
Amazon S3 es un producto de almacenamiento de datos en línea: se cargan archivos en S3 y se obtiene una URL única para cada archivo. Si bien es fácil de usar y económico, no siempre es el más rápido para recuperar archivos almacenados.

Amazon CloudFront funciona con S3 pero copia archivos de S3 al borde exterior de los servidores de Amazon, lo que permite una rápida recuperación.

CloudFront brinda una URL única para los archivos almacenados que no solo apunta a una única copia de su archivo, sino que también almacena el archivo de forma redundante en varias ubicaciones geográficas. Los sistemas de Amazon apuntan la URL a la ubicación más cercana según el navegador de cada cliente, lo que puede acelerar la experiencia de descarga. CloudFront también incluye funciones adicionales para la transmisión rápida de audio y video, lo que lo convierte en una excelente opción para las empresas multimedia en línea.

## Amazon CloudFront
Lo hablaremos en otra ocasión …

![Alt Text](https://media4.giphy.com/media/ui1hpJSyBDWlG/giphy.gif)



