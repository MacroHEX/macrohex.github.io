---
layout: post
title:  "Controla tu Pc con Home Assistant"
categories: [self-hosted, truenas scale, truenas, homeassistant, automatization]
tags: [servers, web, cloud, self-hosted, homeassistant, automatization]
date: 2022-07-05 19:00
---

![https://github.com/LAB02-Research/HASS.Agent](https://repository-images.githubusercontent.com/420055307/d090b8e8-ebae-4129-97f3-5d7c79398531)

## HASS.Agent

Es un cliente de Windows para Home Assistant, desarrollado en .NET 6 por [LAB02](https://github.com/LAB02-Research).

Fue creado para recibir notificaciones en la PC desde Home Assistant y para poder realizar acciones directamente desde la misma.

## Capturas
### Notificaciones

| Ejemplos de las notificaciones |  |
| ----------- | ----------- |
| ![](https://i.imgur.com/hG8hnnM.png) | ![](https://i.imgur.com/mk8WfLG.gif) |

### Interfaz

![](https://i.imgur.com/bMC7aO8.png)

## Instalación

La instalación es sencilla, descargamos el [último instalador](https://github.com/LAB02-Research/HASS.Agent/releases/latest/download/HASS.Agent.Installer.exe), lo ejecutamos y listo!

## Configuración

### Home Assistant

Primero que nada necesitamos instalar a tráves de HACS.

* [HASS.Agent Notifier](https://github.com/LAB02-Research/HASS.Agent-Notifier)
* [HASS.Agent MediaPlayer](https://github.com/LAB02-Research/HASS.Agent-MediaPlayer) 

![HACS](https://i.imgur.com/9S3kplD.png)

Ahora debemos añadir a nuestro configuration.yaml las líneas

```yaml
notify:
  - name: "Nombre PC"
    platform: hass_agent_notifier
    resource: http://ipdelequipo:5115/notify
```

Validamos nuestra configuración y reiniciamos.
![](https://i.imgur.com/7GkduEq.png)

> Solo reiniciar si la configuración es valida de otra forma podemos quedar bloqueados de la interfaz web.
{: .prompt-warning}

Ahora necesitaremos un token para poder realizar la conexión con nuestro equipo.
Nos dirigimos a nuestro usuario de Home Assistant y generamos un nuevo token de acceso de larga vida.

### Windows

Introducimos nuestra dirección de home assistant.

Por ejemplo: https://tunombre.duckdns.org:8123/ y en api pegamos el token que generamos.

![](https://i.imgur.com/PDXT2Ze.png)