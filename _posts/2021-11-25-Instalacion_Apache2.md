---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Configuración básica de Apache II
---


# Configuración básica de Apache II

## Tarea 2

### Utilización de directorios virtuales

Actualizamos los repositorios con Kali. Instalamos Apache.


Crearemos el directorio wiki dentro de /usr/share

```bash
mkdir /usr/share/wiki
```
![Captura](/assets/img/Captura.PNG)

Creamos el fichero index.php

```php
<?php
echo "Mi página de la wiki"
?>
```
![Captura1](/assets/img/Captura1.PNG)

Pondremos el siguiente contenido en mydomain.conf:

```bash
Alias /wiki /usr/share/wiki
	<Directory /usr/share/wiki/>
		DirectoryIndex index.php
	</Directory>
```
![Captura2](/assets/img/Captura2.PNG)

Pondremos la siguiente dirección en el navegador para que nos aparezca la página de la wiki:

```http
http://mydomain.local/wiki
```
![Captura3](/assets/img/Captura3.PNG)