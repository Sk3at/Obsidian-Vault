![](../../Images/Pasted%20image%2020231116202945.png)
Un primer escaneo nos arroja informacion sobre los puertos abiertos
![](../../Images/Pasted%20image%2020231116203412.png)
Realizamos un nuevo escaneo sobre los puertos disponibles
![](../../Images/Pasted%20image%2020231116203436.png)
También ponemos a correr un gobuster y un nikto
![](../../Images/Pasted%20image%2020231116203457.png)
Dentro de la enumeracion de gobuster vemos lo siguiente
![](../../Images/Pasted%20image%2020231116203522.png)
Asi que nos dirigimos a la web y revisamos su codigo fuente para verificar si encontramos algo interesante (no encontramos nada), asi que revisamos ese phpMyAdmin
![](../../Images/Pasted%20image%2020231116203646.png)
Una consola de logeo, intentamos realizar una iSQL pero no fue exitosa, asi que revisamos el otro directorio que encontro gobuster, el /v2 en donde tambien tenemos un panel de login
![](../../Images/Pasted%20image%2020231116204306.png)
Como no tenemos credenciales podemos registrarnos con credenciales inventadas
![](../../Images/Pasted%20image%2020231116204421.png)
Una vez dentro
![](../../Images/Pasted%20image%2020231116204503.png)
Revisamos hasta encontrar que podemos realizar un cambio de contraseña dentro de ResetUser
![](../../Images/Pasted%20image%2020231116204558.png)
Si podemos capturar la petición del cambio de contraseña tal ves podemos realizar un cambio de contraseña en la cuenta del administrador para tener mayor acceso, para intentarlo debemos saber el correo del administrador, luego de unos minutos revisando la pagina dimos con los siguiente
![](../../Images/Pasted%20image%2020231116204806.png)
Tenemos el correo, así que abrimos burp e intentamos interceptar el cambio de contraseña de nuestro usuario para modificarlo por el del administrador
![](../../Images/Pasted%20image%2020231116205012.png)
Como vemos, interceptamos la petición y la misma no se encuentra correctamente sanitizada, por lo que podemos modificarla con el correo de admin y así obtener acceso a esa cuenta.
![](../../Images/Pasted%20image%2020231116205134.png)
Una vez modificada la enviamos e intentamos ingresar como admin
![](../../Images/Pasted%20image%2020231116205228.png)
Ahora podemos intentar subir un revshell en el apartado para subir imágenes
![](../../Images/Pasted%20image%2020231116205605.png)
Esto debemos hacerlo con nuestro burp para poder capturar la ubicación a donde se sube el revshell
![](../../Images/Pasted%20image%2020231116205915.png)
![](../../Images/Pasted%20image%2020231116205928.png)
Nuestro archivo se subirá dentro de
![](../../Images/Pasted%20image%2020231116210100.png)
Asi que antes de dale a forward, vamos a abrir un netcat en nuestro equipo local.
Al dirigirnos al directorio profileimages vemos que tiene el listado deshabilitado
![](../../Images/Pasted%20image%2020231116210336.png)
Por lo que nos referimos entonces a nuestro archivo rev.php
![](../../Images/Pasted%20image%2020231116210359.png)
![](../../Images/Pasted%20image%2020231116210413.png)
Perfecto, ya estamos dentro, ahora debemos encontrar la forma de escalar privilegios aunque no sin antes estabilizar la terminal con el siguiente comando
	python3 -c 'import pty;pty.spawn("/bin/bash")'
Luego de utilizar el CVE-2021-4034 nos convertimos en root
![](../../Images/Pasted%20image%2020231116211322.png)
ls /root



