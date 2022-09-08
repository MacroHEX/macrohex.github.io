---
layout: post
title:  "Instalando Hugo Framework"
categories: [self-hosted, hugo, webpage]
tags: [servers, web, cloud, self-hosted]
date: 2022-09-08 17:00
---

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017550218092363786/2d69f7699c2f3b58.png)

Para probar nuevas cosas instalé el Framework de Hugo, al igual que jekyll (lo que utilizo en esta página) Hugo es un generador de sitios webs estaticos.

Hugo cuenta con uan increíble velocidad, flexibilidad y es de código abierto.

## Instalación

### Chocolatey (Windows)

Utilizando el administrador de paquetes Chocolatey en Windows podemos instalar Hugo con una simple línea:

```powershell
choco install hugo -confirm
```

>Si instalamos [node.js](https://nodejs.org/) nos instalará chocolatey automaticamente 
{: .prompt-tip}

>Para más métodos de instalación visitar la [página oficial](https://gohugo.io/getting-started/installing)
{: .prompt-info}

## Creando un Nuevo Sitio

Nos dirigimos al directorio donde queremos crear nuestro proyecto y en la terminal ingresamos

```powershell
hugo new site {nombre-del-sitio}
```

Para este ejemplo estaré creando una segunda página para mi documentación bajo el nombre de documentacion:

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017550946726846474/WindowsTerminal_PG70mu7KAF.png)

Esto creará nuestro directorio `documentacion` al cual ingresaremos con

```powershell
cd documentacion
```

## Añadiendo Temas

Descargamos el tema de GitHub y lo añadimos al directorio de `themes`:

```powershell
# Para inicializar el directorio
git init 

# Para descargar la carpeta independiente
git clone https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

# Para descargar la carpeta como un submodulo
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

```

Luego añadimos el tema a nuestro archivo `config.toml`

```powershell
echo "theme = 'ananke'" >> .\config.toml
```

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017554493409333289/WindowsTerminal_irDbDZ3yC1.png)

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017554605695057950/WindowsTerminal_np2XHtWIBZ.png)

>En este ejemplo estoy utilizando la plantilla ananke, cada plantilla cuenta con su propio directorio con archivo de configuración de ejemplo en `themes\{tema}\exampleSite\config.toml`
{: .prompt-info}

## Añadiendo Contenido

Podemos añadir contenido manualmente creando un archivo en la carpeta `content/<CATEGORY>/<FILE>/<FORMAT>` y añadir el metadata individualmente, o podemos utilizar el comando `new` que nos genera el metadata automaticamente:

```powershell
hugo new posts/mi-primer-post.md
```

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017554107176865812/WindowsTerminal_cK0QW4Z7yY.png)

## Editando Contenido

Para editar nuestro contenido podemos utilizar el editor de nuestra preferencia, en esta ocasión estaré utilizando Visual Code ejecutando `code .` desde el directorio.

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017563003660538038/WindowsTerminal_ZZSRjWSCTS.png)

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017562855396089886/Code_4wIqtQVdUp.png)

>Los borradores no serán publicados, actualiza la cabecera a `draft: false` Más info [aquí](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)
{: .prompt-info}

## Iniciando el Servidor

Ejecutaremos el comando permitiendo la visualización de los borradores:

```powershell
hugo server -D -p {numero-de-puerto}
```

![](https://cdn.discordapp.com/attachments/1017550158428389376/1017564194989674586/unknown.png)

Ingresamos a nuestro sitio en **http://localhost:{numero-de-puerto}/**

Ahora podremos añadir, editar y eliminar nuestros contenidos, un simple refresco de la página debería actualizar los cambios.

En caso de no actualizarse detendremos el servidor con Ctrl+C y lo volveremos a ejecutar.

## Personalizando el Tema

### Configuración del sitio

Abrimos el archivo ``config.toml`` con un editor de texto:

```
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ananke'
```

- Reemplazamos el campo en `title` por nuestro título para la página.
- Si vamos a subir la página a un dominio modificamos el campo en `baseURL` a la URL de nuestro dominio y para evitar problemas con el protocolo utilizamos `//midominio.com/`
- En este caso cambimo el campo de `languageCode = 'en-us'` a `languageCode = 'es-es'` para tenerlo en español. 

>Debemos recordar que cada tema tiene su propio `config.toml` de ejemplo para la configuración
{: .prompt-info}

## Generando la Página Estática

Es solo correr este comando:

```powershell
hugo -D
```
>La salida será en el directorio ``./public/`` por defecto
{: .prompt-info}