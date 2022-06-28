---
layout: post
title:  "Instalando TrueNAS Scale"
categories: [self-hosted, truenas scale, truenas]
tags: [servers, web, cloud, self-hosted]
---
![](https://www.linuxadictos.com/wp-content/uploads/TrueNASSCALE-Infographics.png)

TrueNAS Scale es un sistema operativo basado en Linux que proporciona servicios de almacenamiento en red. 

Es un sistema operativo gratuito, open-source y de software libre que permite convertir una computadora personal en un soporte de almacenamiento accesible desde red, por ejemplo para almacenamientos masivos de información, música, backups, etc. Además de añadir el poder desplegar aplicaciones en contenedores de docker, el uso de kubernetes y hasta virtualizacion de servicios u otros sistemas.

## Instalación

Lo primero que debemos hacer es ir a la página de [<span style="color:#0095d5">TrueNAS Scale</span>](https://www.truenas.com/download-truenas-scale/) y descargar la última versión estable de la misma.

Utilizamos [<span style="color:white">baelena</span><span style="color:#a5de37">Etcher</span>](https://www.balena.io/etcher/) para crear el USB Booteable.

Una vez creado conectamos el USB a la computadora para iniciar el proceso, mientras inicia presiona la tecla para seleccionar el dispositivo booteable.

Selecciona el dispositivo para bootear.
> Si no se reconoce el USB prueba conectandolo en otro puerto
{: .prompt-tip}

Una vez se haya iniciado el instalador, sigue estos pasos:

Selecciona Install/Upgrade.
![](https://www.truenas.com/docs/images/SCALE/SCALEInstallMainScreen.png)

Selecciona el disco para la instalación.
![](https://www.truenas.com/docs/images/CORE/12.0/InstallDriveScreen.png)
> Es recomendable realizar una instalación espejada por redundancia aunque no es necesaria.
{: .prompt-tip}


Selecciona Yes.
![](https://www.truenas.com/docs/images/CORE/12.0/InstallWarningScreen.png)

Selecciona Fresh Install para realizar una instalación limpia de TrueNAS SCALE. **Esto borrará todo el disco seleccionado**
![](https://www.truenas.com/docs/images/CORE/12.0/InstallWarningScreen.png)

Si el disco tiene suficiente espacio libre, puedes escoger asignar un partición de intercambio para mejorar el rendimiento.
![](https://www.truenas.com/docs/images/CORE/12.0/InstallPartitionScreen.png)

Introduce una contraseña para el usuario ``root`` para loguearse en la interfaz web.
![](https://www.truenas.com/docs/images/CORE/12.0/InstallPasswordScreen.png)

Luego de seguir estos pasos, reinicia el sistema y retira el medio de instalación.

## Primer Logueo

En un equipo conectado a la misma red local del sistema TrueNAS, intruduce la dirección IP en un navegador para conectarte a la intefaz web.

> Puedes asignar una IP fija desde el router utilizando la MAC del equipo.
{: .prompt-info}

Ejemplo:

``https://10.0.0.x``

``https://10.10.10.x``

``https://192.168.100.x``

![](https://www.truenas.com/docs/images/SCALE/LoginSCALE.png)

Escribe ``root`` en el usuario y la contraseña que creaste anteriormente.

Luego de loguearte, verás el Dashboard del sistema.

Este Dashboard muestra información sobre la versión instalada, uso de los componentes del sistema, y tráfico de red.

![](https://i.imgur.com/RVkaVGV.png)

Desde aquí tendrás acceso a todas las opciones que TrueNAS ofrece.

## Creando nuestra primera Pool

La sección de Storage tiene controles para crear pools, snapshots y manejo de los discos.

![](https://www.truenas.com/docs/images/SCALE/StorageSCALE.png)

Para crear una pool vamos Storage > Pools y seleccionados ADD.

Como inicialmente no tendremos ninguna seleccionamos Create new pool y CREATE POOL para abrir el administrador.

![](https://www.truenas.com/docs/images/CORE/13.0/CreatePoolScreen.png)

Escribimos un nombre para la pool.

> No utilices nombres con espacios porque esto podría causar problemas.
{: .prompt-info}