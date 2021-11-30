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



## Tarea 3

### Redirección

Captura del archivo urdomain.conf con la linea del redirect

```bash
sudo nano /etc/apache2/sites-available/urdomain.conf
Redirect /ieselcaminas https://www.ieselacminas.org
```

![imagen1](/assets/img/imagen1.png)

Vamos al navegador y abrimos el apartado Network al hacer Inspeccionar en la página web (A veces tarda un poco)

![image2](/assets/img/image2.png)



## Tarea 4

### Error personalizado

Captura del archivo urdomain.conf con la linea del redirect

Captura del archivo urdomain.conf con la linea del redirect

```bash
sudo nano /var/www/html/urdomain/errorpers.html
```

```html
<html>
<head>
<meta charset="utf-8">
<title>Te has equivocao de página</title>
</head>
<body>
Paice que te has equivocado de dirección, en teoria esto debería ser un error 404. Aquí lo tienes :)
</body>
</html>
```

![imagen5](/assets/img/imagen5.png)

Vamos al fichero de configuración del dominio y añadimos la siguiente linea (importante añadir la barra lateral al inicio del fichero.html, ya que si no, no lo reconoce como una ruta)

```bash
sudo nano /etc/apache2/sites-available/urdomain.conf
ErrorDocument 404 /errorpers.html
```

![imagen3](/assets/img/imagen3.png)

Y comprobamos que funciona:

![imagen4](/assets/img/imagen4.png)
