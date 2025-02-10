# Máquina Oopsie

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 10.129.130.140

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 10.129.130.140

![alt text](image-1.png)

### Fuzzing web

gobuster dir -t 200 -u http://10.129.130.140/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-7.png)

### Burp suite

Interceptamos la petición con burpsuite

![alt text](image-3.png)

entonces entramos a: http://10.129.130.140/cdn-cgi/login/ e iniciamos sesión como guest (invitado)

![alt text](image-2.png)

![alt text](image-4.png)

modificamos la cookie

![alt text](image-5.png)

### Intrusión

![alt text](image-6.png)

me puse en escucha con netcat:

![alt text](image-8.png)

vi los usuarios del sistema:

![alt text](image-9.png)

en /var/www/html/cdn-cgi/login vi un archivo db.php

![alt text](image-10.png)

cambie al usuario robert:

![alt text](image-11.png)

El usuario robert pertenece al grupo bugtracker. Veamos qué ficheros podemos ejecutar por ser miembros de este grupo:

![alt text](image-12.png)

### Escalar privilegios

al ejecutar el binario:

![alt text](image-14.png)

entonces hice lo siguiente

el archivo cat contiene lo siguiente:

/bin/sh

![alt text](image-13.png)