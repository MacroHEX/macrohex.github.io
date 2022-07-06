---
layout: post
title:  "Generando y Añadiendo clave SSH"
categories: [github, ssh]
tags: [github, ssh]
date: 2022-07-06 14:00
---

![ssh](https://i.imgur.com/NPLkGEj.png)

Para poder autenticarnos con GitHub y no utilizar un token podemos utilizar una clave SSH, utilizando esto podemos utilizar una contraseña más simple para realizar nuestros cambios.

## Generando una nueva Clave SSH
### Windows

1. Abrimos Git Bash
2. Copiamos el texto de abajo reemplazando el correo por nuestro correo de GitHub.

    `ssh-keygen -t ed25519 -C "your_email@example.com"`

    > Si utilizas un sistema legacy que no soporte el algoritmo Ed25519, utiliza:
    `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
    {: .prompt-info}

Esto generará nuestra nueva Clave SSH, utilizando nuestro correo como etiqueta.

1. Cuando te pida una dirección para guardar la clave, presiona Enter. Esto guardará la clave en la dirección por defecto.

    `> Enter a file in which to save the key (/c/Users/you/.ssh/id_algorithm):[Press enter]`

2. En la terminal, escribe una contraseña para la clave.

    ```terminal
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
    ```

### Linux
1. Abrimos la Terminalk
2. Copiamos el texto de abajo reemplazando el correo por nuestro correo de GitHub.

    `ssh-keygen -t ed25519 -C "your_email@example.com"`

    > Si utilizas un sistema legacy que no soporte el algoritmo Ed25519, utiliza:
    `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
    {: .prompt-info}

Esto generará nuestra nueva Clave SSH, utilizando nuestro correo como etiqueta.

1. Cuando te pida una dirección para guardar la clave, presiona Enter. Esto guardará la clave en la dirección por defecto.

    `> Enter a file in which to save the key (/home/you/.ssh/id_ed25519_sk): [Press enter]`

2. En la terminal, escribe una contraseña para la clave.

    ```terminal
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
    ```

## Añadiendo la Clave a nuestra cuenta de GitHub
1. Copiamos la clave generada.
    `cat ~/.ssh/id_ed25519.pub`
    > Aquí podriamos usar el comando `clip` pero por alguna razón a mi no me funciona.
    {: .prompt-info}
2. En la esquina superior derecha, hacemos clic en nuestra foto de perfil y clic en **Settings**
   ![](https://docs.github.com/assets/cb-34573/images/help/settings/userbar-account-settings.png)
3. En la sección de "Access" clic en **<i class="fal fa-key"></i> SSH and GPG keys**.
4. Clic en **New SSH key** o **Add SSH key**.
5. En el campo de "Tittle" añadimos una descripción para la nueva clave. Por ejemplo como estoy utilizando un equipo Windows puedo llamar a la clave "Windows Personal".
6. Pega tu clave en el campo de "Key".   
    ![](https://docs.github.com/assets/cb-24796/images/help/settings/ssh-key-paste.png)
7. Clic en **Add SSH key**.   
    ![](https://docs.github.com/assets/cb-2803/images/help/settings/ssh-add-key.png)
8.  Si se solicita introduce tu contraseña.    
    ![](https://docs.github.com/assets/cb-14481/images/help/settings/sudo_mode_popup.png)
9. Listo!

Para más documentación [aquí](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)