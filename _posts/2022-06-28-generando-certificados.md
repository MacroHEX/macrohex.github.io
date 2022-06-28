---
layout: post
title:  "Generando Certificados SSL Autofirmados"
categories: [self-hosted, certificate, openSSL]
tags: [self-hosted, cloud, certificate, security, openSSL]
date: 2022-06-28 17:00
---

![](https://i.imgur.com/fZNF73s.png)

Un problema común con el que podemos encontrarnos durante nuestra travesia montando nuestro Home Lab es que nuestras webs figuren como una conexión ``No segura``.

![](https://i.imgur.com/ARv5Qn5.png)

Esto es debido a que no contamos con un certificado SSL, por decirlo de una manera resumida el certificado SSL es un poco de código en el servidor web que asegura que la conexión sea segura. Cuando la página web contacta a tu servidor, el certificado habilita una conexión encriptada.

> Los certificados autofirmados son recomendados para la red local no para servicios públicos.
{: .prompt-tip}

## Generando los Certificados Autofirmados

### Generamos una Autoridad de Certificación (CA)

Utilizaremos [OpenSSL](https://www.openssl.org/) para generar nuestros certificados.

Viene instalado por defecto en las distribuciones de Linux pero también puede realizarse desde Powershell en Windows.

1. Generamos una clave RSA
```bash
openssl genrsa -aes256 -out ca-key.pem 4096
```

    > ``-aes256`` es la encriptación de 256 bits
    {: .prompt-info}

2. Generamos un Certificado Público del CA
```bash
openssl req -new -x509 -sha256 -days 365 -key ca-key.pem -out ca.pem
```

    > Como vamos a utilizar el certificado internamente podemos aumentar la validez del certificado.
    {: .prompt-tip}

### Generando el Certificado

1. Creamos una clave RSA
```bash
openssl genrsa -out cert-key.pem 4096
```

2. Creamos una Solicitud de Firma de Certificado (CSR)
```bash
openssl req -new -sha256 -subj "/CN=yourcn" -key cert-key.pem -out cert.csr
```

    > Anteriormente el sujeto era importante para la validación pero ya no, así que podemos poner lo que queramos en ``"/CN=yourcn"``.
    {: .prompt-tip}

3. Creamos un archivo `extfile` con los nombres alternativos
```bash
echo "subjectAltName=DNS:your-dns.record,IP:257.10.10.1" >> extfile.cnf
# opcional
echo extendedKeyUsage = serverAuth >> extfile.cnf
```

    > Aquí ingresamos nuestro DNS e IP a las que queremos validar.
    {: .prompt-tip}    
    > Podemos utilizar wildcards en el DNS tales como *.direccion.
    {: .prompt-tip}

4. Creamos el Certificado
```bash
openssl x509 -req -sha256 -days 365 -in cert.csr -CA ca.pem -CAkey ca-key.pem -out cert.pem -extfile extfile.cnf -CAcreateserial
```    

    > Nuevamente podemos aumentar la validez del certificado.
    {: .prompt-tip}

    ```bash
    cat cert.pem > fullchaim.pem
    cat ca.pem >> fullchaim.pem
    ```   

    > Creamos un archivo fullchaim que contenga las dos claves que necesitamos.
    {: .prompt-info}


    Copiar cert-key.pem
    Copiar fullchaim.pem

<!-- ## Certificate Formats

X.509 Certificates exist in Base64 Formats **PEM (.pem, .crt, .ca-bundle)**, **PKCS#7 (.p7b, p7s)** and Binary Formats **DER (.der, .cer)**, **PKCS#12 (.pfx, p12)**.

### Convert Certs

COMMAND | CONVERSION
---|---
`openssl x509 -outform der -in cert.pem -out cert.der` | PEM to DER
`openssl x509 -inform der -in cert.der -out cert.pem` | DER to PEM
`openssl pkcs12 -in cert.pfx -out cert.pem -nodes` | PFX to PEM -->

## Verificar Certificados
```bash
openssl verify -CAfile ca.pem -verbose cert.pem
```

## Instalar la Autoridad de Certificación (CA) en root CA

### En Debian & Derivados
- Mover el CA (`ca.pem`) en `/usr/local/share/ca-certificates/ca.crt`.
- Actualizar la librería de certificados con:
```bash
sudo update-ca-certificates
```

Para más documentación [aquí](https://wiki.debian.org/Self-Signed_Certificate) y [aquí.](https://manpages.debian.org/buster/ca-certificates/update-ca-certificates.8.en.html)

### En Fedora
- Mover el CA (`ca.pem`) en `/etc/pki/ca-trust/source/anchors/ca.pem` or `/usr/share/pki/ca-trust-source/anchors/ca.pem`
- Ahora ejecuta (con sudo si es necesario):
```bash
update-ca-trust
```

Para más documentación [aquí.](https://docs.fedoraproject.org/en-US/quick-docs/using-shared-system-certificates/)

### En Arch
System-wide – Arch(p11-kit) (De la wiki de arch)
- Ejecuta (Como root)
```bash
trust anchor --store myCA.crt
```
- El certificado será escrito en /etc/ca-certificates/trust-source/myCA.p11-kit y los directorios "legacy" se actualizarán automáticamente.
- Si recibes el error "no configured writable location" o similar, importa el CA manualmente:
- Copia el certificado en el directorio /etc/ca-certificates/trust-source/anchors
- y entonces
```bash 
update-ca-trust
```
[wiki](https://wiki.archlinux.org/title/User:Grawity/Adding_a_trusted_CA_certificate)

### En Windows

Asumiento que el directorio a nuestra Autoridad de Certificacion (CA) es `C:\ca.pem`, ejecutamos:
```powershell
Import-Certificate -FilePath "C:\ca.pem" -CertStoreLocation Cert:\LocalMachine\Root
```
- Cambia `-CertStoreLocation` a `Cert:\CurrentUser\Root` en caso de que quieras confiar en los certificados solo para el usuario logueado.

O

En la Terminal, ejecuta:
```sh
certutil.exe -addstore root C:\ca.pem
```

- `certutil.exe` es una herramienta integrada que agrega confianza en todo el sistema.

### En Android

Los pasos exactos cambian entre dispositivos, aquí va una guía generalizada:
1. Abrir las configuraciones
2. Ubicar la sección `Encryption and Credentials` Normalmente ubicada en `Settings > Security > Encryption and Credentials`
3. Seleccionar `Install a certificate`
4. Seleccionar `CA Certificate`
5. Ubicar el archivo `ca.pem` en la memoria utilizando el administrador de archivos.
6. Seleccionarlo.
7. Listo!

> Tengo mi teléfono en inglés así que no se como son las opciones en español :3
{: .prompt-info}