---
layout: post
title:  "Jellyfin una alternativa Open-source a Plex"
categories: [self-hosted, media, open-source]
tags: [self-hosted, cloud, web, media]
date: 2022-06-28 14:00
---

![](https://play-lh.googleusercontent.com/SxdWPR-oZQt9tqph0pyU62_CbyfdQX9g1R5_Nd_vwdkV0IIDceNsytVgdzyHHJGdAwM)

Jellyfin es solución multimedia construida por la comunidad.

Transmite a cualquier dispositivo desde tu propio servidor, sin trabas. Tus archivos, tu servidor, a tu manera.

## Instalación

Jellyfin cuenta con varios medios de instalación y versiones Estables e Inestables.

En esta oportunidad voy a instalarlo en mi equipo con Windows para aprovechar el codificador NVENC de mi tarjeta gráfica.

> Si tenemos un NAS con una gráfica para el encodeo podemos instalar Jellyfin allí
{: .prompt-tip}

Pasos: 

* Visitamos la [página oficial](https://jellyfin.org/downloads/#windows) y seleccionamos nuestro instalador, en este caso utilizaré ``installer/jellyfin_10.8.1_windows-x64.exe``

* Ingresamos en el navegador nuestra dirección local más el puerto 8096 para ingresar a la interfaz web. ``http://SERVER_IP:8096``

> Por el momento solo podremos utilizar http porque para configurar el https necesitamos generar una certificado SSL y utilizar un proxy inverso.
{: .prompt-info}

* Seguimos el asistente de instalación

    * Las librerías y usuarios pueden ser añadidos más adelante desde el dashboard.
    * Recuerda el usuario y la contraseña.

* Ahora podemos proteger nuestro servidor
    * Crea un certificado SSL y añadela en la página de **Networking**
    * Pon tu servidor tras un [proxy inverso](https://jellyfin.org/docs/general/networking/index.html#running-jellyfin-behind-a-reverse-proxy).
    * Solo permite conexiones locales y evita liberar puertos.

> Si solo queremos utilizarlo localmente podemos permitir la salida al puerto 8096 en nuestro firewall. Solo si no vamos a acceder al servidor externamente.
{: .prompt-warning}

* Disfruta!

## Añadiendo librerías

Las librerías son una colección virtual de media que pueden contener archivos de varios directorios en el servidor.

La primera vez que abras el servidor aparecerá una página para crear librerías, pero pueden añadirse o eliminarse en cualquier momento desde las configuraciones.

Loguea en la interfaz web en el navegador.

En el menu que aparece:

* Admin > Dashboard.
* Server > Libraries.
* Selecciona "Add Media Library".

El servidor ahora escaneará los directorios y añadirá tu media.

Habrá una barra indicando el progreso.

> Pueden utilizarse diferentes medios como películas, shows y música.
También soporta libros o fotos.
{: .prompt-info}

> Utiliza directorios separados para cada tipo de medios para evitar problemas con los resultados de metada.
{: .prompt-tip}