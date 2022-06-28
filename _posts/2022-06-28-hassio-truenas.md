---
layout: post
title:  "Home Assistant OS en TrueNAS Scale"
categories: [self-hosted, truenas scale, truenas, homeassistant, automatization]
tags: [servers, web, cloud, self-hosted, homeassistant, automatization]
---

![](https://i.imgur.com/LS80XNH.png)

Home Assistant es un software gratuito y de código abierto para la automatización del hogar diseñado para ser un sistema de control central para dispositivos domésticos inteligentes con un enfoque en el control local y la privacidad. 

## El Problema

![](https://i.imgur.com/QIHpjWv.png)

Visita [https://www.home-assistant.io/installation/](https://www.home-assistant.io/installation/) para más información

Como podemos observar la versión que tiene todas las funcionalidades que podemos necesitar es ``Home Assistant OS`` pero la única forma de correrlo es virtualizandolo.

Así que utilizaremos la capacidad de virtualización de TrueNAS Scale para crear una instancia de Home Assistant OS.

## Instalando Home Assistant OS en TrueNAS Scale
Creamos un directorio en una de nuestras pools, en este caso voy a utilizar mi dataset vms:

![](https://i.imgur.com/E8Ic8dx.png)

Creamos el directorio utilizando el shell de TrueNAS:

```bash
/mnt/<Nombre-Pool>/<Nombre-Dataset>
mkdir hass
cd hass/
```

Ahora una vez dentro del directorio que acabamos de crear utilizamos wget para obtener el archivo ova.
```bash
wget https://github.com/home-assistant/operating-system/releases/download/8.2/haos_ova-8.2.ova
```

> Visitar la página de [releases](https://github.com/home-assistant/operating-system/releases/) para seleccionar la última versión del sistema operativo.
{: .prompt-tip}

Una vez descargado el archivo lo descomprimimos utilizando tar:
```bash
tar -xvf haos_ova-8.2.ova
```

Ahora convertimos el vmdk a una imagen raw, utilizando el directorio completo para la fuente:
```bash
qemu-img convert -f vmdk -O raw /mnt/<Nombre-Pool>/<Nombre-Dataset>/hass/home-assistant.vmdk hassos.img
```

Creamos un Zvol utilizando la interfaz web de TrueNAS.
![](https://i.imgur.com/ccWL95C.png)
> Hay que asegurarse de que el volumen sea lo suficientemente grande para que dd pueda completarse, en este caso utilice 50Gib
{: .prompt-tip}

Ahora utilizamos dd para escribir la imagen en nuestro Zvol.
```bash
dd if=hassos.img of=/dev/<Nombre-Pool>/<Nombre-Zvol>
```

Creamos una máquina virtual utilizando la interfaz gráfica y seleccionamos nuestro zvol como disco.
![](https://i.imgur.com/FKI0Jep.png)

Requisitos minimos recomendados:
* 2GB RAM
* 32Gb Almacenamiento
* 2vCPU

Todo esto puede ser expandido según la necesidad de cada sistema.

Iniciamos la máquina virtual y esperamos que termine el proceso de instalación.
![](https://i.imgur.com/5WQQvU2.png)