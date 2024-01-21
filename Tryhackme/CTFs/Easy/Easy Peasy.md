![](../../Images/Pasted%20image%2020231208111223.png)
Un primer escaneo con nmap nos arroja informacion sobre los puertos abiertos
![](../../Images/Pasted%20image%2020231208112025.png)
Con una segunda enumeración visualizamos los servicios ejecutándose en esos puertos
![](../../Images/Pasted%20image%2020231208112054.png)
Vemos dos servidores web corriendo en la maquina victima y un ssh por lo que ejecutamos un whatweb para cada uno de ellos.
![](../../Images/Pasted%20image%2020231208112340.png)
Lo siguiente es analizar cada uno de ellos realizando un ataque de fuerza bruta para listar posibles directorios dentro de la web.
En la primera enumeracion con gobuster sobre el puerto 80 nos encuentra dos resultados
![](../../Images/Pasted%20image%2020231208112643.png)
El robots no contiene nada de interes, asi que revisamos el hidden y realizamos una nueva enumeracion con gobuster.
![](../../Images/Pasted%20image%2020231208112721.png)
En este nuevo directorio al revisar el codigo fuente encontramos lo siguiente:
![](../../Images/Pasted%20image%2020231208112810.png)
Parece estar en base64 asi que lo decodificamos y obtenemos nuestra primera flag.
![](../../Images/Pasted%20image%2020231208112856.png)
Volvemos a enumerar sobre el directorio whatever pero no encontramos nada, asi que pasamos al siguiente servicio web que se encuentra en el puerto 65524, primero revisamos su codigo fuente  tiene un mensaje escondido.
![](../../Images/Pasted%20image%2020231208114255.png)
El mismo se encuentra codificado en base 63 y al decodificarlo vemos lo siguiente
![](../../Images/Pasted%20image%2020231208114416.png)
Al dirigirnos al directorio nuevamente parece haber un mensaje oculto
![](../../Images/Pasted%20image%2020231208114502.png)
Al romper ese mensaje con john y el diccionario brindado en el desafío encontramos lo siguiente
![](../../Images/Pasted%20image%2020231208114848.png)
Ahora realizamos un gobuster y vemos que hay disponible un robots.
![](../../Images/Pasted%20image%2020231208113237.png)
Al revisar el robots vemos un mensaje
![](../../Images/Pasted%20image%2020231208113302.png)
En principio trate de enumerar la web especificando ese user agent pero no me llevo a ningun lado, al mirar mas de cerca el mismo parece ser un md5.
El decrypt lo realize con https://md5hashing.net/hash/md5/
![](../../Images/Pasted%20image%2020231208115956.png)
Al revisar nuevamente el código de la pagina vemos la flag 3
![](../../Images/Pasted%20image%2020231208120140.png)
Volviendo al directorio que encontramos, podemos descargar la imagen pequeña ya que parece sospechosa.
![](../../Images/Pasted%20image%2020231208120306.png)
Utilizamos las herramientas exiftool para ver la metadata e intentamos extraer directamente con steghide, al hacerlo nos pidio una contraseña. la cual es la misma que conseguimos anteriormente con john.
![](../../Images/Pasted%20image%2020231208120510.png)
Al revisar el archivo encontramos un nombre de usuario y una contraseña codificada en binario.
![](../../Images/Pasted%20image%2020231208120539.png)
Al decodificarla vemos
![](../../Images/Pasted%20image%2020231208120629.png)
Al ingresar por ssh con nuestras nuevas credenciales vemos la user flag la cual parece estar codificada
![](../../Images/Pasted%20image%2020231208120915.png)
Antes de intentar decodificarla intentaremos convertirnos en root, por lo que probamos con sudo -l pero no encontramos nada, asi que revisamos las tareas cron.
![](../../Images/Pasted%20image%2020231208121020.png)
Al revisar el script vemos que somos el propietario del mismo y es corrido por el usuario root cada cierto tiempo.
![](../../Images/Pasted%20image%2020231208121126.png)
Ahora tenemos muchisimas opciones para convertirnos en root, una de ellas es agregar una revshell al archivo, otra es modificar los permisos del usuario boring para que pueda utilizar cualquier comando como root sin contraseña.
Vamos a utilizar la segunda opcion, para ello ejecutamos el siguiente comando
	printf '#! /bin/bash\necho "boring ALL=NOPASSWD:ALL" >> /etc/sudoers' > /var/www/.mysecretcronjob.sh
![](../../Images/Pasted%20image%2020231208121358.png)
Ahora esperamos unos momentos a que root ejecute la tarea y tendremos acceso total.
![](../../Images/Pasted%20image%2020231208121433.png)
![](../../Images/Pasted%20image%2020231208121444.png)
![](../../Images/Pasted%20image%2020231208121718.png)
Ahora decodificamos la user flag la cual se encuentra codificada con ROT13
![](../../Images/Pasted%20image%2020231208121657.png)





