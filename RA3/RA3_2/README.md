# RA3_2

Este documento describe los pasos seguidos para superar los niveles low y medium de la herramienta DVWA (Damn Vulnerable Web Application).

# Tasks

* [Primeros Pasos DVWA](#Primeros-Pasos-DVWA)
* [Level Low](#Level-Low)
* [Level Medium](#Level-Medium)

# Primeros Pasos DVWA

Para la instalación y configuración de [DVWA](https://github.com/digininja/DVWA) se han seguido los pasos del siguiente video proporcionado en su repositorio oficial: [Installing DVWA on Kali running in VirtualBox](https://www.youtube.com/watch?v=WkyDxNJkgQ4&ab_channel=RobinWood).

Despues de su instalación y configuración, podremos acceder a DVWA simplemente iniciando el servicio apache2 y la base de datos mariadb.

```
sudo service apache2 start
service mariadb start

# URL acceso: http://localhost/DVWA
```

Una vez dentro, podremos ajustar el nivel de dificultad dentro de la pestaña "DVWA Security".
![image](https://github.com/user-attachments/assets/347bc4f3-5ae2-4496-aab0-7e332ac0eaf2)

# Level Low

## Brute Force
## Command Injection
## Cross Site Request Forgery (CSRF)
## File Inclusion
## File Upload
## SQL Injection
## SQL Injection (Blind)
## Weak Session IDs
## DOM Based Cross Site Scripting (XSS)
## Reflected Cross Site Scripting (XSS)
## Stored Cross Site Scripting (XSS)
## Content Security Policy (CSP) Bypass
## JavaScript Attacks

# Level Medium

## Brute Force
## Command Injection
## Cross Site Request Forgery (CSRF)
## File Inclusion
## File Upload
## SQL Injection
## SQL Injection (Blind)
## Weak Session IDs
## DOM Based Cross Site Scripting (XSS)
## Reflected Cross Site Scripting (XSS)
## Stored Cross Site Scripting (XSS)
## Content Security Policy (CSP) Bypass
## JavaScript Attacks
