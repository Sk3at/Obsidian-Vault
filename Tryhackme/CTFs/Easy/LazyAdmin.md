![](../../Images/Pasted%20image%2020231119023043.png)
Comenzamos realizando un escaneo de los 65535 puertos para verificar cuales se encuentran abiertos
![](../../Images/Pasted%20image%2020231119023211.png)
Ahora realizamos un escaneo para ver la version de los servicios que se encuentran abiertos
![](../../Images/Pasted%20image%2020231119023329.png)
Procedemos a correr un gobuster para obtener directorios de la web mientras la revisamos
![](../../Images/Pasted%20image%2020231119023430.png)
Verificamos en la pagina web si hay algún comentario disponible que nos de mas informacion
![](../../Images/Pasted%20image%2020231119023529.png)
No encontramos nada en el código fuente, pero mientras revisamos, nuestro gobuster finalizo
![](../../Images/Pasted%20image%2020231119023605.png)
Revisamos el directorio
![](../../Images/Pasted%20image%2020231119023659.png)
Realizamos un nuevo gobuster pero dentro de /content
![](../../Images/Pasted%20image%2020231119023820.png)
Vemos que nos encontro varios directorios, los cuales procedemos a revisar.
En /as vemos una pagina de login
![](../../Images/Pasted%20image%2020231119024016.png)
Dentro del directorio /inc vemos una carpeta que se llama mysql_backup y un archivo que se llama lastest.txt
![](../../Images/Pasted%20image%2020231119024358.png)
Vamos a revisar ambos, primero el txt
![](../../Images/Pasted%20image%2020231119024439.png)
Parece ser la versión de sweetrice que se esta ejecutando en la web.
Ahora revisamos dentro del backup de mysql
![](../../Images/Pasted%20image%2020231119024524.png)
Al revisar el archivo parece ser que encontramos la contraseña codificada
![](../../Images/Pasted%20image%2020231119024857.png)
Al revisar que tipo de codigo puede ser con dcode se nos dice que es probable sea MD5
![](../../Images/Pasted%20image%2020231119024930.png)
Asi que nos dirigimos a crackstation e intentamos ver si nos la descifra
![](../../Images/Pasted%20image%2020231119025058.png)
Al intentar ingresar vemos que no es posible ya que intentamos con user admin, probamos con user manager y logueamos de forma exitosa.
![](../../Images/Pasted%20image%2020231119025300.png)
Teniendo nuestras credenciales, revisamos en el navegador si existe algún exploit para sweetrice 1.5.1 y encontramos los siguientes:
![](../../Images/Pasted%20image%2020231119030043.png)
Intentamos utiliza el de Arbitrary File Upload pero no fue exitoso, así que probamos con el de PHP Code Execution. Al leerlo nos encontramos con que desde ads podemos cargar un revshell en php
![](../../Images/Pasted%20image%2020231119030233.png)
Este archivo que subimos, ira a parar a la carpeta inc, donde se encuentran los archivos de ads
![](../../Images/Pasted%20image%2020231119030719.png)
Abrimos un listener antes de abrir el revshell
![](../../Images/Pasted%20image%2020231119030757.png)
Al revisar los comandos que podemos ejecutar como root sin contraseña encontramos que podemos ejecutar perl para un script de itguy (usuario)
![](../../Images/Pasted%20image%2020231119030829.png)
Al revisar el script de perl vemos que se esta ejecutando otro script dentro de /etc.
![](../../Images/Pasted%20image%2020231119030948.png)
Al revisar el mismo vemos que podemos modificar su contenido
![](../../Images/Pasted%20image%2020231119031135.png)
Por lo que lo modificamos para que nos ejecute una bash
![](../../Images/Pasted%20image%2020231119031246.png)
Una vez ejecutamos el comando permitido para nuestro usuario como sudo, nos convertiremos automáticamente en root
![](../../Images/Pasted%20image%2020231119031421.png)
