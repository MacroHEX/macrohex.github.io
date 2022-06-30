---
layout: post
title:  "Instalando el Subsistema de Windows para Linux (WSL)"
categories: [wsl]
tags: [wsl]
date: 2022-06-29 10:00
---

![](https://static.marriedgames.com.br/e5d756ca-wsl-1.jpg)

El Subsistema de Windows para Linux permite a los desarrolladores ejecutar un entorno de GNU/Linux, incluida la mayoría de herramientas de línea de comandos, utilidades y aplicaciones, directamente en Windows, sin modificar y sin la sobrecarga de una máquina virtual tradicional o una configuración de arranque dual.

## ¿Qué podemos hacer con esto?

* Podemos escoger nuestras distros favoritas de la [Tienda de Microsoft](https://aka.ms/wslstore)
* Ejecutar herramientas comunes de línea de comandos, como ``grep``, ``sed``, ``awk`` u otros archivos binarios ELF-64.
* Ejecutar scripts de shell de Bash y aplicaciones de línea de comandos de GNU/Linux, como:
    * Herramientas: vim, emacs, tmux.
    * Lenguajes: NodeJS, Javascript, Python, Ruby, C/C++, C# & F#, Rust, Go, etc.
    * Servicios: SSHD, MySQL, Apache, lighttpd, MongoDB, PostgreSQL.

* Instalar software adicional mediante el administrador de paquetes de distribución de GNU/Linux.
* Invocar aplicaciones de Windows mediante un shell de línea de comandos de tipo UNIX.
* Invocar aplicaciones de GNU/Linux en Windows.

## Versiones

El Subsistema de Windows para Linux cuenta actualmente con dos versiones y la principal diferencia entre WSL1 y WSL2 es que WSL1 cuenta con una capa de compatibilidad para la transferencia de la ejecución del código entre Windows y Linux, en cambio WLS2 está basado en la virtualización de un sistema operativo Linux. Esta máquina virtual se ejecuta en el hipervisor nativo de Windows Hyper-V.

## Instalación

### Prerrequisitos

Debemos contar con Windows 10 versión 2004 o posterior o Windows 11

> Para comprobar la versión y el número de compilación de Windows, seleccione la tecla del logotipo de **Windows + R**, escriba **winver** y seleccione Aceptar. Para actualizar a la versión de Windows más reciente, seleccione **Inicio>Configuración>Windows Update>Buscar actualizaciones.**
{: .prompt-tip}

Debemos revisar que tengamos activa la virtualización en la BIOS de nuestra placa madre.


### Instalando

Realizaremos la instalación de todo lo que necesitamos por medio de PowerShell en modo administrador y a continuación reiniciaremos el equipo.

#### PowerShell
```powershell
wls --install
```

Este comando habilitará los componentes opcionales necesarios, descargará el kernel de Linux más reciente, establecerá WSL 2 como predeterminado e instalará una distribución de Linux automáticamente (Ubuntu de forma predeterminada).

La primera vez que inicie una distribución de Linux recién instalada, se abrirá una ventana de la consola y se le pedirá que espere a que los archivos se descompriman y se almacenen en el equipo. Todos los inicios posteriores deberían tardar menos de un segundo en completarse.

> El comando anterior solo funciona si WSL no está instalado. Si ejecuta ``wsl --install`` y ve el texto de ayuda de WSL, intente ejecutar ``wsl --list --online`` para ver una lista de distribuciones disponibles y ejecute`` wsl --install -d <DistroName>`` para instalar una distribución.
{: .prompt-info}


## Troubleshooting
Si recibimos un error de que no se puede iniciar la virtualización debemos revisar que tengamos activa la opción en la BIOS de nuestro sistema y en `Panel de Control>Programas>Activar o desactivar las características de Windows` y activamos ``Hyper-V``, ``Virtual Machine Platform`` y ``Windows Hypervisor Platform``

> En mi caso necesite activar los 3 para que funcione el Subsistema.
{: .prompt-info}

Para la documentación oficial [aquí](https://docs.microsoft.com/es-es/windows/wsl/install)