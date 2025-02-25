FROM ubuntu:latest

# Herramientas
RUN apt-get update && apt-get install -y \
    apache2 \
    openssl \
    curl \
    nano \
    && apt-get clean

# Activar el módulo SSL de Apache
RUN a2enmod ssl

# Crear el directorio para los certificados SSL
RUN mkdir -p /etc/apache2/ssl

# Generar un certificado SSL auto-firmado
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/apache2/ssl/apache.key \
    -out /etc/apache2/ssl/apache.crt \
    -subj "/C=ES/ST=Castellon/L=Castellon de la Plana/O=IES El Caminas/OU=PPS/CN=www.midomimioseguro.com/emailAddress=your_email@midomimioseguro.com"

# Configurar Apache para usar SSL con el certificado auto-firmado
RUN cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/000-default.conf \
    && sed -i 's|SSLCertificateFile /etc/ssl/certs/ssl-cert-snakeoil.pem|SSLCertificateFile /etc/apache2/ssl/apache.crt|' /etc/apache2/sites-available/default-ssl.conf \
    && sed -i 's|SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key|SSLCertificateKeyFile /etc/apache2/ssl/apache.key|' /etc/apache2/sites-available/default-ssl.conf \
    && sed -i 's|#SSLEngine on|SSLEngine on|' /etc/apache2/sites-available/default-ssl.conf \
    && sed -i 's|ServerAdmin webmaster@localhost|ServerAdmin admin@midominioseguro.com|' /etc/apache2/sites-available/default-ssl.conf \
    && sed -i 's|ServerName www.example.com|ServerName www.midomimioseguro.com|' /etc/apache2/sites-available/default-ssl.conf \
    && echo 'Redirect permanent / https://www.midomimioseguro.com/' >> /etc/apache2/sites-available/000-default.conf

# Habilitar el sitio SSL y reiniciar Apache
RUN a2ensite default-ssl.conf && service apache2 restart

# Exponer el puerto 80 (HTTP) y 443 (HTTPS)
EXPOSE 80 443

# Iniciar Apache en modo foreground
CMD ["apachectl", "-D", "FOREGROUND"]
