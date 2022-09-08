# Amazon Web Services - CloudFront

## Content Delivery Network (CDN) - Red de entrega de contenido
Es una red de entrega de contenido, o una red de servidores distribuidos por el mundo, que sirve páginas web o cualquier otro contenido, basándose en la posición geográfica del usuario y en el origen de los datos a distribuir.

## CloudFront
Amazon CloudFront es un servicio de red de entrega de contenido (CDN) creado para ofrecer un alto rendimiento, seguridad y comodidad para los desarrolladores, que permite acelerar la entrega de contenido web estático y dinámico a los usuarios finales.

Está optimizado para trabajar con otros servicios de AWS, como S3 (almacenamiento), EC2 (computo), ELB (balanceadores de carga), Route 53 (servicio de DNS), Shield (para mitigar ataques DDoS) y Lambda@Edge (para ejecutar código personalizado más cerca de los usuarios).

Tambien trabaja perfectamente con otros servidores fuera de AWS.

## Ventajas de usar un CDN - CloutFront
- Acelera la distribución de contenido estático tales como: .html, .css, .js, imagenes y videos para usuarios finales.
- Tu contenido cacheado en todo el mundo.
- Menos latencia y mejor experiencia de usuario.
- Se paga solo por la transferencia de datos y las solicitudes que realmente use.
- Sin costo de transferencia de datos entre regiones AWS y puntos de distribución CloudFront

### Casos de uso

- Entregue sitios web completos (parte estática y parte dinamica, contenido interactivo, video, etc) de manera rápida y segura, utilizando una red global de localizaciones cercanas (edge) a los usuarios. Las peticiones a su web serán automaticamente enrutadas a la localización mas próxima del usuario, maximizando el rendimiento.
- Acelere la entrega de contenidos dinámicos y las API: Optimice la entrega de contenido web dinámico con la infraestructura de red global de AWS, creada con fines específicos y dotada de numerosas características, que admite la terminación en el borde y los WebSockets.
- Transmita video en directo y en diferido: Inicie transmisiones rápidamente, reprodúzcalas con coherencia y entregue vídeo de alta calidad a cualquier dispositivo con la integración de AWS Media Service y AWS Elemental.
- Distribuya parches y actualizaciones: Ajuste la escala de forma automática para entregar software, parches de juegos y actualizaciones de IoT inalámbricas (OTA) a escala con altas tasas de transferencia.

### ¿Qué necesitamos saber?

#### Edge Locations (localizaciones borde)
- Son las localizaciones de los servidores de AWS más cercanas geográficamente a cada usuario, que van a cachear el contenido del servidor
- El contenido estará cacheado el tiempo indicado en TTL.
- Podemos borrar el contenido cacheado, pero adiciona coste.

![Alt Text](https://github.com/karpalypy/tech-share/blob/main/aws-cloudfront/red-global-cloudfront.png)



#### Origen
- Es el servidor que contiene nuestros datos, que estará en algunas de las regiones de AWS.

#### Distribución
- Es una coleccion de ubicaciones borde (locales, edge), que pueden ser de tipo web (para distribución de sitios web) o de tipo RTMP (para el streaming de video).

[Mas info](https://aws.amazon.com/es/cloudfront/features/?whats-new-cloudfront.sort-by=item.additionalFields.postDateTime&whats-new-cloudfront.sort-order=desc)


