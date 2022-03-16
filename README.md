# Crear host virtuales desde otras fuentes

**Virtual host 000-default.conf**
```
<VirtualHost *:80>
ServerName example.com
DocumentRoot /var/www/html/dominios/public
ErrorLog ${APACHE_LOG_DIR}/error-dominios.log
CustomLog ${APACHE_LOG_DIR}/access-dominios.log combined
RewriteEngine on
RewriteCond /etc/letsencrypt/live/%{SERVER_NAME}/fullchain.pem -f
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```

**Virtual host 000-default-le-ssl.conf**
```
<IfModule mod_ssl.c>
<VirtualHost *:443>
ServerName example.com
DocumentRoot /var/www/html/dominios/public
Include /etc/letsencrypt/options-ssl-apache.conf
SSLCertificateFile /etc/letsencrypt/live/example.com-0001/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/example.com-0001/privkey.pem
</VirtualHost>
Include /certificados/dominios.conf
</IfModule>
```

