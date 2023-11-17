Un primer escaneo nos muestra 4 puertos abiertos
![](../../Images/Pasted%20image%2020231114205700.png)
Ahora realizamos un escaneo mas profundo sobre esos puertos para ver sus versiones
![](../../Images/Pasted%20image%2020231114212136.png)
Vemos que tenemos un smtp en el 25, una web en el 80 y un servidor de correo en los dos restantes, procedemos a revisar la web y dentro del código fuente de la pagina encontramos lo que parece ser un nombre de usuario y una contraseña encriptada.
![](../../Images/Pasted%20image%2020231114212509.png)
Al revisar la contraseña encriptada parece estar en HTML Entity, asi que la decodficiamos con cyberchef
![](../../Images/Pasted%20image%2020231114213255.png)
Ahora que tenemos un nombre de usuario y contraseña intentamos loguearnos y una vez dentro vemos lo siguiente
![](../../Images/Pasted%20image%2020231114214307.png)
Asi que probamos conectarnos a pop3 con nc.
![](../../Images/Pasted%20image%2020231114214418.png)
Vemos que con las credenciales que tenemos fallan, pero podemos intentar realizar un ataque de fuerza bruta ya que sabemos que el usuario boris existe, luego de romper la contraseña de boris nos logueamos ya sea utilizando telnet o netcat
![](../../Images/Pasted%20image%2020231114220753.png)
Dentro vemos 3 mensajes, si abrimos uno por uno encontramos 2 nuevos nombres de usuarios, uno es natalya y otro xenia
![](../../Images/Pasted%20image%2020231114220831.png)
![](../../Images/Pasted%20image%2020231114220840.png)
Realizamos nuevamente un ataque con hydra pero al usuario natalya
![](../../Images/Pasted%20image%2020231114220713.png)
Nos logueamos como el nuevo usuario
Al ver sus mensajes en el segundo conseguimos las credenciales de xenia
![](../../Images/Pasted%20image%2020231114221102.png)
Remarcamos que en el final del mensaje vemos
![](../../Images/Pasted%20image%2020231114221241.png)
Asi que editamos nuestro /etc/hosts
![](../../Images/Pasted%20image%2020231114221336.png)
Dentro de la web nos logueamos como xenia y vemos un mensaje del Dr.Doak
![](../../Images/Pasted%20image%2020231115104757.png)
Probamos utilizar hydra con este nuevo usuario
![](../../Images/Pasted%20image%2020231115104823.png)
Asi que nuevamente nos conectamos a pop3 pero con nuestras nuevas credenciales
![](../../Images/Pasted%20image%2020231115104913.png)
Vemos en su mensaje tanto su usuario y contraseña para la web, asi que nos dirigimos nuevamente alli
Dentro encontramos un archivo
![](../../Images/Pasted%20image%2020231115105116.png)
Asi que lo descargamos y revisamos 
![](../../Images/Pasted%20image%2020231115105153.png)
Dentro del directorio vemos una imagen asi que la descargamos y revisamos
![](../../Images/Pasted%20image%2020231115105317.png)
Al revisarla con exiftool vemos en la descripcion lo que parece ser base64
![](../../Images/Pasted%20image%2020231115105405.png)
Al decodificarla obtenemos 
![](../../Images/Pasted%20image%2020231115105441.png)
Por lo que logueamos en la web como el usuario admin
![](../../Images/Pasted%20image%2020231115105623.png)
Dado que tenemos mayores privilegios en la pagina chequeamos donde podriamos colocar codigo malicioso para obtener una revshell
![](../../Images/Pasted%20image%2020231115110443.png)
![](../../Images/Pasted%20image%2020231115110455.png)
Parece que en aspell podemos colocar codigo
![](../../Images/Pasted%20image%2020231115110750.png)
Para que nos funcione nuestro reverse debemos modificar el spell engine
![](../../Images/Pasted%20image%2020231115110903.png)
Ahora debemos crear por ejemplo un nuevo post para realizar el spell cheker
![](../../Images/Pasted%20image%2020231115111052.png)
![](../../Images/Pasted%20image%2020231115111141.png)
Cuando activemos el comprobador deberiamos obtener en nuestro nc el shell
![](../../Images/Pasted%20image%2020231115111204.png)
![](../../Images/Pasted%20image%2020231115111221.png)
Ahora debemos escalar privilegios, por lo que chequeamos la versión de kernel de la maquina
![](../../Images/Pasted%20image%2020231115113231.png)
Encontramos un exploit de este kernel en exploitdb
![](../../Images/Pasted%20image%2020231115113905.png)
Lo descargamos de forma local y modificamos de gcc a cc la linea que se ve en la imagen
![](../../Images/Pasted%20image%2020231115113842.png)
Ahora seteamos un server con python de forma local y pasamos el exploit a la maquina victima
![](../../Images/Pasted%20image%2020231115114126.png)
![](../../Images/Pasted%20image%2020231115114133.png)
Una vez con nuestro archivo en la maquina victima lo movemos a /tmp, lo compilamos y ejecutamos para convertirnos en root
![](../../Images/Pasted%20image%2020231115115013.png)
Obtenemos nuestra root flag
![](../../Images/Pasted%20image%2020231115115125.png)
