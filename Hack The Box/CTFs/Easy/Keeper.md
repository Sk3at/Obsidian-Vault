![](../../Images/Pasted%20image%2020231208140522.png)
Un primer escaneo nos revela los puertos abiertos
![](../../Images/Pasted%20image%2020231208141211.png)
Ahora realizamos un escaneo para verificar la versión de servicios en ejecución
![](../../Images/Pasted%20image%2020231208141238.png)
Realizamos un reconocimiento de las tecnologías utilizadas en la web
![](../../Images/Pasted%20image%2020231208141306.png)
Realizamos un ataque con gobuster para encontrar directorios en la web y no encontramos nada de utilidad.
Asi que procedemos a revisar la web en la que vemos lo siguiente
![](../../Images/Pasted%20image%2020231208141442.png)
Asi que agregamos el nombre de dominio a nuestro /etc/hosts
![](../../Images/Pasted%20image%2020231208142009.png)
Al hacer click en el enlace se nos redirecciona a un panel de login
![](../../Images/Pasted%20image%2020231208142049.png)
Vemos que la version es RT 4.4.4 asi que buscamos por algunas credenciales por defecto para verificarlas.
![](../../Images/Pasted%20image%2020231208142131.png)
Intentamos ingresar con estas credenciales y estamos dentro
![](../../Images/Pasted%20image%2020231208142210.png)
Al revisar el panel de admin encontramos un usuario y su contraseña inicial.
![](../../Images/Pasted%20image%2020231208142340.png)
Probamos estas credenciales en el servicio ssh
![](../../Images/Pasted%20image%2020231208142437.png)
Ahora que estamos dentro revisamos los posibles vectores de escalación clásicos.
![](../../Images/Pasted%20image%2020231208142552.png)
Como se puede observar no encontramos nada por este lado.
Asi que realizamos un poco de reconocimiento en la maquina, listando los archivos del usuario, dentro encontramos la user flag.
![](../../Images/Pasted%20image%2020231208142737.png)
Realizamos un unzip del archivo RT
![](../../Images/Pasted%20image%2020231208143203.png)
Vemos que se trata de un dump de keepas, asi que podemos pasarlo con python a nuestra maquina atacante.
![](../../Images/Pasted%20image%2020231208143758.png)
![](../../Images/Pasted%20image%2020231208143810.png)
Buscando en google encontramos lo siguiente:
![](../../Images/Pasted%20image%2020231208143841.png)
Podemos realizar un dump de la contraseña maestra gracias al CVE-2023-32784, para ello encontramos un poc
https://github.com/matro7sh/keepass-dump-masterkey
Asi que lo descargamos y ejecutamos
![](../../Images/Pasted%20image%2020231208144209.png)
Ahora que vemos una lista de posibles contraseñas, como las mismas no estan claras intentamos buscar en google una de ellas.
![](../../Images/Pasted%20image%2020231208144303.png)
Ahora intentamos abrir la kdbx con esta contraseña con la herramienta keepass2.
![](../../Images/Pasted%20image%2020231208145223.png)
Una vez abierto vemos un PuTTy key del usuario root
![](../../Images/Pasted%20image%2020231208145143.png)
Asi que la copiamos y utilizamos puttykey para generar un id_rsa.
![](../../Images/Pasted%20image%2020231208145250.png)
Cambiamos los permisos e intentamos utilizar el id_rsa para conectarnos como root por ssh.
![](../../Images/Pasted%20image%2020231208145355.png)
![](../../Images/Pasted%20image%2020231208145404.png)
Obtenemos la root flag.
![](../../Images/Pasted%20image%2020231208145428.png)

![](../../Images/Pasted%20image%2020231208145617.png)




