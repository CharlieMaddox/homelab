# MI PROYECTO PERSONAL DE HOMELAB

> ### ¿Por qué el proyecto? 
> Este proyecto comienza como el resultado de tener computadoras viejitas arrumbadas en casa y la necesidad de aprender todo lo que se pueda respecto a la administración de servidores, así como a usar nuevas tecnologías. Además, surge a demás de querer tener mi propio ecosistema y nube privada.

> ## Comandos utiles


```yml
Desplegar un contenedor desde el arhivo.yml
    docker compose up -d

docker ps -a --format "table {{.ID}}\t{{.Names}}\t{{.Status}}\t{{.Image}}\t{{.Size}}"
 ```

> ## Contenedores


### 1.- File Browser [Dockerhub](https://hub.docker.com/r/filebrowser/filebrowser)
```txt
File Browser es una aplicación web que permite explorar, administrar y compartir archivos de un servidor
de forma sencilla y visual. Funciona como un gestor de archivos accesible desde un navegador, sin 
necesidad de usar SSH o FTP.

📌 Características principales:

✅ Interfaz web intuitiva para navegar por el sistema de archivos.
✅ Subida, descarga y edición de archivos directamente desde el navegador.
✅ Soporte para múltiples usuarios con permisos personalizados.
✅ Integración con autenticación y certificados SSL.
✅ Fácil instalación con Docker o binario independiente.
✅ Es ideal para gestionar archivos en servidores locales o en la nube sin depender de clientes FTP o comandos de terminal. 🚀
```

### 2.- Heimdall [dockerhub](https://hub.docker.com/r/linuxserver/heimdall)
```txt
Heimdall es un panel de inicio personalizable que permite organizar y acceder fácilmente a aplicaciones, 
servicios y sitios web desde una interfaz centralizada. Es especialmente útil en homelabs y servidores, 
ya que permite tener un acceso rápido a herramientas como File Browser, Jellyfin, Nextcloud, Pi-hole, entre otros.

📌 Características principales:
✅ Interfaz limpia y personalizable con iconos y descripciones de cada servicio.
✅ Soporte para enlaces directos a aplicaciones locales o en la nube.
✅ Modo "Enhanced" que muestra información en vivo de ciertos servicios (como carga del sistema o estado de monitoreo).
✅ Fácil instalación con Docker y configuración sin necesidad de base de datos.
```

### 3.- Jellyfin [Dockerhub](https://hub.docker.com/r/jellyfin/jellyfin)

```txt
Jellyfin es un servidor multimedia de código abierto que te permite gestionar y transmitir tu colección de películas, series, música y fotos a cualquier dispositivo sin depender de servicios en la nube como Netflix o Spotify.

📌 Características principales:
✅ Streaming local y remoto: Accede a tu contenido desde PC, móviles, Smart TVs y más.
✅ Transcodificación en tiempo real: Optimiza el contenido para distintos dispositivos.
✅ Soporte para múltiples usuarios: Cada usuario tiene su propia biblioteca y progreso de reproducción.
✅ Clientes en varias plataformas: Apps para Android, iOS, Roku, Fire TV, Kodi y navegadores web.
✅ Sin suscripciones ni restricciones: A diferencia de Plex o Emby, Jellyfin es 100% gratuito y sin funciones premium bloqueadas.
```
### 4.- Nextcloud [Dockerhub](https://hub.docker.com/r/linuxserver/nextcloud)
```txt
Nextcloud es una plataforma de almacenamiento en la nube de código abierto, similar a Google Drive o Dropbox, pero alojada en tu propio servidor. Te permite sincronizar, compartir y proteger archivos, además de ofrecer funciones adicionales como calendarios, contactos, edición de documentos y videollamadas.

📌 Características principales:
✅ Almacenamiento y sincronización de archivos en múltiples dispositivos.
✅ Compartición segura con enlaces protegidos por contraseña y permisos personalizados.
✅ Extensiones y apps para añadir funciones como edición de documentos (Collabora/ONLYOFFICE), notas, correo, calendario, etc.
✅ Cifrado y control de privacidad, sin depender de servicios en la nube de terceros.
✅ Accesible desde cualquier navegador o mediante aplicaciones para Windows, Linux, macOS, Android e iOS.
```
### 5.- Nginx Proxy Manager [Dockerhub](https://hub.docker.com/r/jc21/nginx-proxy-manager)
```txt
Nginx Proxy Manager es una herramienta que simplifica la configuración de Nginx como proxy inverso, permitiéndote redirigir tráfico a diferentes servicios o contenedores de manera fácil y con una interfaz web.

📌 Principales funciones:
✅ Proxy inverso → Redirige tráfico HTTP/HTTPS a diferentes contenedores o servidores.
✅ Gestión de certificados SSL → Soporte nativo para Let’s Encrypt con renovación automática.
✅ Interfaz web → No necesitas editar archivos manualmente.
✅ Autenticación → Protege rutas con usuario y contraseña.
✅ Reglas de redireccionamiento → Personaliza accesos con diferentes dominios o subdominios.
```
### 6.- Uptime Kuma [Dockerhub](https://hub.docker.com/r/linuxserver/nextcloud)
```txt
Uptime Kuma es una herramienta de monitoreo de servidores y servicios que te permite verificar si tus sitios web, contenedores o dispositivos están en línea. Es una alternativa autoalojada y de código abierto a servicios como Uptime Robot.

📌 Características principales:
✅ Monitoreo de múltiples servicios (HTTP, TCP, Ping, DNS, Docker, etc.).
✅ Notificaciones personalizadas en Telegram, Discord, Slack, correo, entre otros.
✅ Historial de disponibilidad con estadísticas y tiempos de respuesta.
✅ Interfaz web moderna y fácil de usar.
✅ Instalación simple con Docker.
```
### 7.- Wallos [Dockerhub](https://hub.docker.com/r/linuxserver/nextcloud)
```txt
Wallos App es una aplicación autoalojada y de código abierto diseñada para gestionar y organizar suscripciones personales, permitiendo un mejor control de pagos recurrentes. Es una alternativa privada a servicios como Truebill o Subby.

📌 Características principales:
✅ Registro y seguimiento de suscripciones con fechas de vencimiento.
✅ Organización de pagos por categorías personalizables.
✅ Soporte para múltiples monedas y conversión automática.
✅ Notificaciones de próximos pagos a través de correo, Telegram y Discord.
✅ Interfaz web intuitiva con opciones de personalización.
✅ Instalación sencilla con Docker. 
```
### 8.- Firefly III [Dockerhub](https://hub.docker.com/r/fireflyiii/core)
```txt
Firefly III es una aplicación de gestión financiera autoalojada y de código abierto que permite realizar un seguimiento detallado de ingresos, gastos, presupuestos y cuentas bancarias. Es una alternativa privada a herramientas como YNAB o Mint.

📌 Características principales:
✅ Gestión de cuentas bancarias con soporte para múltiples monedas.
✅ Presupuestos y control de gastos con categorías personalizables.
✅ Importación de transacciones desde archivos CSV, OFX, QIF, JSON, entre otros.
✅ Informes detallados con gráficos y análisis financieros.
✅ API integrada para automatizar transacciones y conectar otras aplicaciones.
✅ Instalación sencilla con Docker.
```
### numero.- Nueva Herramienta [Dockerhub](https://hub.docker.com)
```txt
Descripcion de lo que es y/o hace la herramienta que se esta implementando 
```