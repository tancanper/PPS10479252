# RA3_1

Este documento describe los pasos necesarios para aplicar medidas de hardening en un servidor Apache. Se configurarán certificados SSL/TLS, un OWASP y se implementarán mejores prácticas de seguridad. Además, se crearán imágenes Docker.

# Tasks

* [TASK_1](#Preparación del Entorno): Preparación del Entorno.
* [TASK_2](#URL_TASK_2): Apache Hardening

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
3. Instalar Docker y Docker Compose
```
sudo apt install docker.io -y
sudo systemctl enable --now docker
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
7. Instalar Fail2Ban
```
sudo apt install fail2ban -y
```
# Apache Hardening
El hardening de Apache es un proceso que sirve para reducir los ataque en un servidor web. Esto incluye deshabilitar módulos innecesarios, configurar reglas de seguridad y aplicar restricciones en las solicitudes HTTP.

# Webgrafía
