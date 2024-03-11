![](../../Images/Pasted%20image%2020231215015331.png)
Un primer escaneo nos muestra los puertos abiertos en la maquina victima.
![](../../Images/Pasted%20image%2020231215015554.png)
En el segundo escaneo vemos la versión de los servicios en ejecución
![](../../Images/Pasted%20image%2020231215015617.png)
Como se puede observar, en la web se encuentra corriendo un wordpress.
Antes realizaremos una enumeración de la web con whatweb para verificar tecnologías y gobuster para listar directorios.
![](../../Images/Pasted%20image%2020231215015838.png)
![](../../Images/Pasted%20image%2020231215015859.png)
Comprobamos el directorio hidden mientras ponemos a correr wpscan para realizar una enumeración de usuarios de wordpress.
La enumeración de usuarios con worpress la logramos con el siguiente comando
	wpscan --url http://10.10.154.205/ -e 
Esto nos arroja los siguientes resultados
![](../../Images/Pasted%20image%2020231215020726.png)
Al revisar el directorio hidden encontramos un mensaje de philip diciendo lo siguiente
![](../../Images/Pasted%20image%2020231215020819.png)
Asi que ahora podemos intentar realizar un ataque de fuerza bruta, esto lo podemos hacer tanto con wpscan como con hydra, para realizarlo con hydra debemos interceptar la petición para poder forjar de forma correcta el comando. En este caso utilizamos wpscan sobre el usuario c0ldd
	wpscan --url http://10.10.154.205/ -P /usr/share/wordlists/rockyou.txt --usernames c0ldd
![](../../Images/Pasted%20image%2020231215025033.png)
Asi que ahora intentamos loguear a wordpress con nuestras nuevas credenciales.
Dentro confirmamos que el rol de nuestro usuario es administrador
![](../../Images/Pasted%20image%2020231215025210.png)
Asi que podemos editar alguna de las paginas para obtener un shell reverso con php.
En este caso editamos la pagina 404
![](../../Images/Pasted%20image%2020231215025404.png)
Una ves cargado nuestro revshell de php en la pagina 404, debemos dirigirnos hacia ella por medio del tema que modificamos
![](../../Images/Pasted%20image%2020231215032105.png)
![](../../Images/Pasted%20image%2020231215032113.png)
Ahora que estamos dentro toca escalar privilegios, pero no sin antes upgradear nuestra shell
![](../../Images/Pasted%20image%2020231215032259.png)
Dentro de la maquina, luego de realizar un poco de reconocimiento vemos que esta disponible el archivo de configuración de wordpress dentro de /var/www/html
![](../../Images/Pasted%20image%2020231215032522.png)
Al leerlo encontramos la contraseña del usuario c0ldd
![](../../Images/Pasted%20image%2020231215032559.png)
Asi que nos convertimos en el usuario
![](../../Images/Pasted%20image%2020231215032633.png)
Al ejecutar sudo -l vemos que tenemos varias opciones para convertirnos en root
![](../../Images/Pasted%20image%2020231215032730.png)
En este caso lo hicimos mediante ftp
![](../../Images/Pasted%20image%2020231215032840.png)
Ahora toca obtener ambas flags.

