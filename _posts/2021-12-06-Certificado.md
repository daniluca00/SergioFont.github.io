---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Instalación de un certificado digital en Apache
---

# Instalación de un certificado digital en Apache



## Paso 1

```bash
sudo a2enmod ssl
sudo service apache2 restart
```
![image-20211202162521308](/assets/img/image-20211202162521308.png)



## Paso 2

```bash
sudo mkdir /etc/apache2/ssl
sudo openssl req -x509 -nodes -days 365 \ 
-newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```

![image-20211202163151989](/assets/img/image-20211202163151989.png)

Miramos dentro de /etc/apache2/ssl, donde estarán la clave y el directorio

![image-20211202163447344](/assets/img/image-20211202163447344.png)



## Paso 3

```bash
sudo nano /etc/apache2/sites-available/default-ssl.conf

<IfModule mod_ssl.c>
    <VirtualHost _default_:443>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        SSLEngine on
        SSLCertificateFile /etc/ssl/certs/ssl-cert-snakeoil.pem
        SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key
        <FilesMatch "\.(cgi|shtml|phtml|php)$">
                        SSLOptions +StdEnvVars
        </FilesMatch>
        <Directory /usr/lib/cgi-bin>
                        SSLOptions +StdEnvVars
        </Directory>
        BrowserMatch "MSIE [2-6]" \
                        nokeepalive ssl-unclean-shutdown \
                        downgrade-1.0 force-response-1.0
        BrowserMatch "MSIE [17-9]" ssl-unclean-shutdown
    </VirtualHost>
</IfModule>

```

Después de modificar las siguientes línea quedaría así:

![image-20211202165946380](/assets/img/image-20211202165946380.png)



## Paso 4

Modificaremos el fichero /etc/hosts:

![image-20211202170213378](/assets/img/image-20211202170213378.png)



## Paso 5

Habilitamos el archivo default-ssl.conf y reiniciamos el servicio.

```bash
sudo a2ensite default-ssl.conf
sudo service apache2 restart
```



## Paso 6

Ponemos la URL https://www.midominioseguro.com y nos sacará el certificado. 

![image-20211207170931505](/assets/img/image-20211207170931505.png)



Si le damos a más información comprobaremos que aparecen más datos sobre el certificado

![image-20211207171144456](/assets/img/image-20211207171144456.png)

## Paso 7

Dentro de default-ssl.conf añadimos las siguientes líneas

```bash
<VirtualHost *:80>
	ServerName www.midominioseguro.com
	Redirect / https://www.midominioseguro.com/	    
</VirtualHost>
```

Comprobación del método GET 302 Redirect

![image-20211207181803275](/assets/img//image-20211207181803275.png)

