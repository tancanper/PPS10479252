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

En este nivel deberemos ejecutar un ataque de fuerza bruta. Para empezar deberemos descargarnos una lista de palabras llamada [Rockyou.txt](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt&ved=2ahUKEwiu-qu5o9-MAxUYSPEDHf9pEIsQFnoECAkQAQ&usg=AOvVaw3snAERl1mU6Ccr4WFEazBd) e instalar la [herramienta hydra](#Instalación-de-Hydra).

Una vez descargada, ejecutaremos el siguiente comando:
```
hydra -l admin -P rockyou.txt 127.0.0.1 http-get-form "/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:Username and/or password incorrect.:H=Cookie: security=low; PHPSESSID=rt5o26sooph0v8p5nuarofj346"
```

A través de él obtendremos las credenciales admin:password.

![image](https://github.com/user-attachments/assets/07d70a74-fdeb-4d10-a206-501f52fbd295)

## Command Injection

En este nivel, nos permiten hacer un ping a una IP o dominio. Por ejemplo, vamos a hacer ping al localhost.

![image](https://github.com/user-attachments/assets/6d79e83f-06ca-44b1-bd6f-1df002417717)

Además de esto, vamos a probar si podemos introducir otro comando. Para ello, utilizaremos la tubería "|".

```
localhost | ls
```
Mediante este comando se mostrarán los archivos del directorio.

![image](https://github.com/user-attachments/assets/8ead9e5e-ade3-4848-8492-339615eff4c9)



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

# Herramientas

## Instalación de Hydra
1. Instalación de dependencias.
   ```
   sudo apt update
   sudo apt install git build-essential libssl-dev zlib1g-dev
   ```
3. Clonar repositorio de Hydra.
   
   ```
   git clone https://github.com/vanhauser-thc/thc-hydra.git
   ```
5. Entrar al directorio y compilar.
   
   ```
   cd thc-hydra
   ./configure
   make
   sudo make install
   ```
7. Prueba de funcionamiento.
   
   ```
   hydra -h
   ```
