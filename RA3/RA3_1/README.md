# RA3_1

Este documento describe los pasos necesarios para aplicar medidas de hardening en un servidor Apache. Se configurarán certificados SSL/TLS, un OWASP y se implementarán mejores prácticas de seguridad. Además, se crearán imágenes Docker.

# Tasks

* [TASK_1](#Preparación-del-Entorno): Preparación del Entorno.
* [TASK_2](#Apache-Hardening): Apache Hardening.
* [TASK_3](#Certificados-SSL): Certificados SSL.
* [TASK_4](#Mejores-Prácticas-y-Docker): Mejores Prácticas y Docker.

# Preparación del Entorno
## Instalación de Herramientas
1. Actualizar paquetes y repositorios
```
sudo apt update && sudo apt upgrade -y
```
2. Instalar Apache
```
sudo apt install apache2 -y
```
3. Instalar Docker
```
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```
4. Instalar OpenSSL para gestión de certificados
```
sudo apt install openssl -y
```
5. Instalar UFW y permitir tráfico HTTP y HTTPS
```
sudo apt install ufw -y
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```
6. Instalar ModSecurity para Apache
```
sudo apt install libapache2-mod-security2 -y
sudo a2enmod security2
sudo systemctl restart apache2
```
7. Instalar las CRS de OWASP
```
sudo apt install modsecurity-crs -y
```
8. Instalar Fail2Ban
```
sudo apt install fail2ban -y
```
# Apache Hardening
El hardening de Apache es un proceso que sirve para reducir los ataque en un servidor web. Esto incluye deshabilitar módulos innecesarios, configurar reglas de seguridad y aplicar restricciones en las solicitudes HTTP.
## CSP

## Web Application Firewall
## OWASP
## Evitar ataques DDOS

# Certificados SSL

# Mejores Prácticas y Docker

# Conclusión

# Webgrafía
* Hardening del servidor. (2021, 1 marzo). https://psegarrac.github.io/Ciberseguridad-PePS/tema3/seguridad/web/2021/03/01/Hardening-Servidor.html.
* Certificado digital. (2020, 8 noviembre). https://psegarrac.github.io/Ciberseguridad-PePS/tema1/practicas/2020/11/08/P1-SSL.html.
* Kumar, C. (2024, 21 diciembre). Apache Web Server Hardening and Security Guide. Geekflare. https://geekflare.com/cybersecurity/apache-web-server-hardening-security/.
* Kumar, C. (2024a, mayo 15). Guía de seguridad y endurecimiento del servidor web Nginx. Geekflare Spain. https://geekflare.com/es/nginx-webserver-security-hardening-guide/.

