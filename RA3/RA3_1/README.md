# RA3_1

Este documento describe los pasos necesarios para aplicar medidas de hardening en un servidor Apache. Se configurarán certificados SSL/TLS, un OWASP y se implementarán mejores prácticas de seguridad. Además, se crearán imágenes Docker.

# Tasks

* [TASK_1](#Preparación-del-Entorno): Preparación del Entorno.
* [TASK_2](#Apache-Hardening): Apache Hardening.
* [TASK_3](#Certificados-SSL): Certificados SSL.
* [TASK_4](#Mejores-Prácticas-y-Docker): Mejores Prácticas y Docker.

# Preparación del Entorno
## Instalación de Herramientas
1. Actualizar paquetes y repositorios.
```
sudo apt update && sudo apt upgrade -y
```
2. Instalar Apache.
```
sudo apt install apache2 -y
```
3. Instalar Docker.
```
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```
4. Instalar OpenSSL para gestión de certificados.
```
sudo apt install openssl -y
```
5. Instalar UFW y permitir tráfico HTTP y HTTPS.
```
sudo apt install ufw -y
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```
6. Instalar ModSecurity para Apache.
```
sudo apt install libapache2-mod-security2 -y
```
7. Instalar las CRS de OWASP.
```
sudo apt install modsecurity-crs -y
```
8. Instalar Fail2Ban.
```
sudo apt install fail2ban -y
```
# Apache Hardening
El hardening de Apache es un proceso que sirve para reducir los ataque en un servidor web. Esto incluye deshabilitar módulos innecesarios, configurar reglas de seguridad y aplicar restricciones en las solicitudes HTTP.
## CSP
1. Editar el archivo de configuración del sitio en Apache.
```
sudo nano /etc/apache2/sites-available/000-default.conf
```
2. Añadir la directiva CSP dentro del bloque <VirtualHost>.
```
<VirtualHost *:80>
    ...
    Header set Content-Security-Policy "default-src 'self'; script-src 'self'; object-src 'none';"
    ...
</VirtualHost>
```
![CSP - Config](https://github.com/user-attachments/assets/104b413d-0129-49cc-b4ba-44e82fcb542d)

3. Habilitar el módulo de encabezados y reiniciar Apache.
```
sudo a2enmod headers
sudo systemctl restart apache2
```
![CSP - headers](https://github.com/user-attachments/assets/bfb22460-02ee-4a79-b91e-c03114b4511c)

## Web Application Firewall
1. Habilitar el módulo de seguridad en Apache.
```
sudo a2enmod security2
```
2. Reiniciar Apache para aplicar los cambios.
```
sudo systemctl restart apache2
```
3. Configurar las reglas de ModSecurity.
```
sudo cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
sudo nano /etc/modsecurity/modsecurity.conf
# Buscar la siguiente línea: SecRuleEngine DetectionOnly; Cambiar DetectionOnly por On.
```
![Modsecurity](https://github.com/user-attachments/assets/973114a6-f0aa-46e2-a844-93fa4ac177d3)

4. Volver a reiniciar Apache.
5. Comprobar funcionamiento.

   5.1. Crer un archivo de prueba en el DocumentRoot de Apache.
   ```
   sudo nano /var/www/html/prueba.php
   ```
   ![WAF](https://github.com/user-attachments/assets/57bda759-0c8f-4aa7-bcc1-cb9a1c5932f8)
   5.2. Ataque XSS. Escribir en el campo de texto:
   ```
   <script>alert('Ataque XSS');</script>
   ```
   ![WAF - Ataque XSS](https://github.com/user-attachments/assets/22dc17ba-8ac9-4713-9f34-780d7569a909)

## OWASP
1. Clonar el repositorio de OWASP CRS.
```
git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git
```
2. Mover los archivos de configuración a la carpeta de ModSecurity.
```
cd owasp-modsecurity-crs
sudo mv crs-setup.conf.example /etc/modsecurity/crs-setup.conf
sudo mv rules/ /etc/modsecurity
```
3. Comprobar que el archivo security2.conf contenga las siguientes lineas:
```
<IfModule security2_module>
	# Default Debian dir for modsecurity's persistent data
	SecDataDir /var/cache/modsecurity
	SecRuleEngine On
	# Keeping your local configuration in that directory
	# will allow for an easy upgrade of THIS file and
	# make your life easier
    IncludeOptional /etc/modsecurity/*.conf
	Include /etc/modsecurity/rules/*.conf	
</IfModule>
```
4. Comprobar funcionamiento.

   4.1 Modificar el archivo de configuración del Host Virtual.
   ![OWASP - Host Virtual](https://github.com/user-attachments/assets/b1e049c5-cf30-4e19-8d52-4f1fac94ce41)

5. 
## Evitar ataques DDOS

# Certificados SSL

# Mejores Prácticas y Docker

# Conclusión

# Webgrafía
* Hardening del servidor. (2021, 1 marzo). https://psegarrac.github.io/Ciberseguridad-PePS/tema3/seguridad/web/2021/03/01/Hardening-Servidor.html.
* Certificado digital. (2020, 8 noviembre). https://psegarrac.github.io/Ciberseguridad-PePS/tema1/practicas/2020/11/08/P1-SSL.html.
* Kumar, C. (2024, 21 diciembre). Apache Web Server Hardening and Security Guide. Geekflare. https://geekflare.com/cybersecurity/apache-web-server-hardening-security/.
* Kumar, C. (2024a, mayo 15). Guía de seguridad y endurecimiento del servidor web Nginx. Geekflare Spain. https://geekflare.com/es/nginx-webserver-security-hardening-guide/.

