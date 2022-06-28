---
layout: post
title:  "Conoce Jekyll - El Generador de Sitio Web Estático"
categories: [self-hosted, jekyll, webpage]
tags: [servers, web, cloud, self-hosted]
---

![](https://miro.medium.com/max/1400/1*xhVXlPsI9x1zF4_mK5gFbw.png)

Jekyll es una generador de sitio web estático que transforma texto plano en un bonito sitio web estático. Puede ser utilizado para un sitio de documentación, un blog, un sitio de evento, o básicamente para lo que quieras. Es rápido, seguro, fácil de utilizar y de código libre. 


Deja tu ⭐ al repo de [jekyll](https://github.com/jekyll/jekyll) y el repo de [Chrirpy theme](https://github.com/cotes2020/jekyll-theme-chirpy)


## Prerrequisitos

* [Ruby](https://www.ruby-lang.org/en/downloads/)
* [RubyGems](https://rubygems.org/pages/download)
* [GCC](https://gcc.gnu.org/install/)
* [Make](https://www.gnu.org/software/make/)


### Ubuntu/Debian
```bash
sudo apt update && sudo apt upgrade
sudo apt-get install ruby-full build-essential zlib1g-dev
```

## Creando la web utilizando una plantilla
Visita: [https://github.com/cotes2020/jekyll-theme-chirpy#quick-start](https://github.com/cotes2020/jekyll-theme-chirpy#quick-start)

Tras crear un repositorio basado en la plantilla, clonamos el repositorio

> No clonar el repositorio estando en super usuario.
{: .prompt-tip }

``` bash
# Con SSH
git clone git@github.com:<TU-USUARIO>/<NOMBRE-REPO>.git

# Con HTTPS
git clone https://github.com/<TU-USUARIO>/<NOMBRE-REPO>.git
```


Entonces instalamos las dependencias

``` bash
cd nombre-repo
bundle
```

Luego de realizar los cambios, commit y push a git

``` bash
git add .
git commit -m "Algunos cambios"
git push
```

## Edición

Utilicé VS Code con WSL
```bash
code .
```

## Comandos de Jekyll

Inicializar el servidor local

``` bash
$ bundle exec jekyll s
```

## Creando una Publicación
Jekyll sigue una nomenclatura para [nombrar las páginas y publicaciones](https://jekyllrb.com/docs/posts/)

Crear un archivo en ``_posts`` con el formato:

AÑO-MES-DIA-TITULO.md

### Por ejemplo:
2022-06-26-documentacion.md

2022-06-30-pruebas.md

> Verificar la fecha y hora, así como la zona horaría si no se ve la publicación.
{: .prompt-tip }

## Vinculando archivos locales

Vincular una imagen:

```md
... como se puede apreciar en la captura:
![Una captura](/assets/screenshot.png)
```

Vincular un archivo:

```md
... puedes [descargar el PDF](/assets/algo.pdf) aquí.
```

## Ejemplos de Markdown
Si queremos ayuda con el markdown, revisa la [tabla](https://www.markdownguide.org/cheat-sheet/)

Para más sintaxis para el tema de Chirpy vista la demo de como hacer publicaciones

[https://chirpy.cotes.page/posts/write-a-new-post/](https://chirpy.cotes.page/posts/write-a-new-post/)