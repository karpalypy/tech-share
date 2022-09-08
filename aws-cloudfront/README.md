# Amazon Web Services - CloudFront

## Content Delivery Network (CDN) - Red de entrega de contenido
Es una red de entrega de contenido, o una red de servidores distribuidos por el mundo, que sirve páginas web o cualquier otro contenido, basándose en la posición geográfica del usuario y en el origen de los datos a distribuir.

## CloudFront ☁️
Amazon CloudFront es un servicio de red de entrega de contenido (CDN) creado para ofrecer un alto rendimiento, seguridad y comodidad para los desarrolladores, que permite acelerar la entrega de contenido web estático y dinámico a los usuarios finales.

Está optimizado para trabajar con otros servicios de AWS, como S3 (almacenamiento), EC2 (computo), ELB (balanceadores de carga), Route 53 (servicio de DNS), Shield (para mitigar ataques DDoS) y Lambda@Edge (para ejecutar código personalizado más cerca de los usuarios).

## Ventajas de usar un CDN - CloutFront
- Acelera la distribución de contenido estático tales como: .html, .css, .js, imagenes y videos para usuarios finales.
- Tu contenido cacheado en todo el mundo.
- Menos latencia y mejor experiencia de usuario.
- Se paga solo por la transferencia de datos y las solicitudes que realmente use.
- Sin costo de transferencia de datos entre regiones AWS y puntos de distribución CloudFront.

AWS tiene mas de 400 **Puntos de Presencia** - **PoP** (Data Center que está ubicado en algun lugar del globo, que no tiene necesariamente todos los servicios de AWS (A diferencia de una Región), pero si tiene la capacidad de proveer servicios de computo, especialmente servicios de almacenamiento de forma distribuida. Existen otros Data Center llamados Cache regionales, que son extensiones de las regiones con el unico proposito de almacenar cópias de archivos.

## ¿Cómo funciona?
Cuando se accede a un contenido, el camino desde el origen de la petición (browser) hasta llegar al servidor que aloja dicho contenido (que suele estar en otra región) suele ser largo, y suele pasar por diferentes servidores (hops):
  
>browser ➡️ ISP local ➡️ ISPs del país ➡️ hops internacionales (cables submarinos) ➡️ ISPs de otra región ➡️ ... ➡️ contenido
  
Con CloudFront, cuando se carga el contenido por primera vez, se cachea, y dura un TTL disponible para todos los usuarios que lo consuman.

![Alt Text](https://github.com/karpalypy/tech-share/blob/main/aws-cloudfront/flujo-entrega-contenido.png)

1. Usuario solicita un archivo (DNS): todo parte con un request hacia un archivo. 
2. El DNS asociado al dominio sabe que quien responde es CloudFront. Route 53 le dice al browser que la IP que busca es de CloudFront. 
3. CloudFront verifica si el archivo existe y lo entrega.
4. Si no se encuentra en el cache local, Cloudfront:
  -  Hace la petición al origen (un bucket S3, una maquina en EC2, incluso un servidor externo).
  -  Genera una copia local y entrega la respuesta al cliente que hizo la petición. Desde ahí se tiene el archivo cacheado en el PoP para futuras peticiones (TTL). EL servidor de DNS decide que PoP usar (por proximidad geográfica).

  
### ¿Qué pasa con contenido dinámico que no se puede cachear porque cambia con el tiempo?
- Brinda conexión mas estable, que aunque tengas que ir al origen, lo harás de manera mas expedita a través del *Backbone* de AWS.

### Integración nativa con otros servicios AWS para Aplicaciones Seguras y Resilientes

- **Shield Advanced** 🛡️: ofrece protección contra ataques de tipo *DDoS*. Como cloudfront está entre el cliente y el servidor, es capaz de detectar este tipo de ataque. Hace un filtrado inteligente de tráfico, permitiendo solo las peticiones reales de clientes, y evitando que las peticiones de robots o maquinas zombies 🧟 lleguen al servidor. La versión **Shield** es sin costo, y la **Shield Advance** es paga. La diferencia está en que con Advance, tienes un equipo de AWS de personas disponibles 24/7 (SRT), que monitorea y visualiza todo el perfil de tráfico que pasa por tu distribución y pueden ejecutar acciones de mitigación y de respuesta de forma inmediata.

- **AWS WAF**  - Web Application Firewall 🔥: se puede generar reglas que te protegen contra otros tipos de ataque: SQL Injection, Cross-site scripting (XSS), otros.     

-  **AWS WAF Bot Control** 🤖: deja que pasen los *bot buenos* (crawlers o arañas web 🕷️ - indexado de contenido web en buscadores) y bloquea los *bot malos* (scrapers 🧛, que capturan info para disponibilizarla en otros sitios). 


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


#### Servidor de Origen
- Es el servidor que contiene nuestros datos originales. Puede ser un servicio de AWS como Amazon S3, Amazon EC2, ELB, MediaStore, o incluso puede ser un servidor fuera de AWS.

#### Política de protocólo de lectura
- Protocolo para establecer conexion entre fuente de contenido y el browser. Puede ser HTTP o HTTPS.

#### Periodo de Expiración (TTL)
- Tiempo en segundos que determina el tiempo de vida del caché. Se configura en los archivos origen, a través de cabeceras de control de cache, y se usa para determinar si es necesario preguntar al origen por un archivo actualizado.

#### Distribución
- Es una coleccion de ubicaciones borde (locales, edge), que pueden ser de tipo web (para distribución de sitios web) o de tipo RTMP (para el streaming de video).

[Mas info](https://aws.amazon.com/es/cloudfront/features/?whats-new-cloudfront.sort-by=item.additionalFields.postDateTime&whats-new-cloudfront.sort-order=desc)

[Sesión con Adler Oliveria](https://www.youtube.com/watch?v=eY80b-aC3WU)


