---
layout: post
title:  "Configurando Duck DNS en Home Assistant"
categories: [self-hosted, truenas scale, truenas, homeassistant, automatization]
tags: [servers, web, cloud, self-hosted, homeassistant, automatization, duckdns]
date: 2022-06-28 11:00
---

![](https://i.imgur.com/0CMreMJ.png)

Duck DNS es un servicio gratuito que se encarga de dirigir direcciones IP a subdominios del tipo duckdns.org.

El servicio de DDNS asocia nuestra IP pública a un dominio. De esta forma podemos acceder a nuestro servicio sin necesidad de escribir nuestra IP.

## Preparación

Nos logueamos en Duck DNS utilizando cualquiera de los métodos disponibles.
![](https://i.imgur.com/XoRA6Tm.png)

Ahora necesitamos realizar el port forwarding para poder ver nuestra instancia de Home Assistant en Internet.

>Pasamos el puerto 8123 a 8123 en el protocolo TCP y 443 a 8123 también en TCP
{: .prompt-info}

>Instrucciones de Port Forwading [aquí](https://portforward.com/router.htm)
{: .prompt-tip}

## Instalación

Primero nos dirigimos a la tienda de add-ons e instalamos Duck DNS
![](https://i.imgur.com/EzLtOqj.png)

Seleccionamos ``Start on boot`` y ``Watchdog``

Antes de iniciarlo, nos dirigimos a la pestaña de configuración y editamos en YAML.
>La nueva versión de Home Assitant cuenta con una interfaz para cargar los datos pero por alguna razón no me aceptó la configuración al hacerlo con la interfaz.
{: .prompt-tip}

Añadimos nuestro dominio de DuckDNS junto al token que nos dió y cambiamos ``accept_terms: false`` a ``accept_terms: true``

```yaml
domains:
  - midomio.duckdns.org
token: mitoken
aliases: []
lets_encrypt:
  accept_terms: true
  algo: secp384r1
  certfile: fullchain.pem
  keyfile: privkey.pem
seconds: 300
```

Iniciamos el servico y refrescamos el Log hasta que leamos que se generó el certificado.


Una vez que se haya generado el certificado debemos añadir esto a  ``configuration.yaml``

```yaml
# Loads default set of integrations. Do not remove.
default_config:

# Añadimos esto
http:
  ssl_certificate: /ssl/fullchain.pem
  ssl_key: /ssl/privkey.pem
  ip_ban_enabled: true
  login_attempts_threshold: 5
```

Vamos a ``Developer Tools`` validamos la configuración y reiniciamos Home Assistant

![](https://i.imgur.com/IUUULSS.png)

>Desde este momento la IP de nuestro Home Assistant va a cambiar a ``https://midominio.duckdns.org:8123``
{: .prompt-warning}

>Vamos a poder seguir conectandonos localmente entrando a ``https://ip-del-equipo:8123.`` pero como generamos el certificado para el dominio de duckdns nos va a decir que el sitio no es seguro.
{: .prompt-tip}