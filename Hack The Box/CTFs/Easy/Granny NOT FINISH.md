Luego de un escaneo inicial verificamos que unicamente se encuentra abierto el puerto 80, por lo que realizamos un nuevo escaneo para verificar la version del servicio en ejecucion.
![](../../Images/Pasted%20image%2020240420095249.png)
Como se puede observar se trata de un IIS 6.0, al realizar un busqueda con searchsploit vemos que posee algunas vulnerabilidades, sobre todo de webdav.
![](../../Images/Pasted%20image%2020240420095420.png)
Antes de intentar utilizar alguno de estos exploits, realizaremos una búsqueda de directorios de la web para ver si encontramos algo de interés.
![](../../Images/Pasted%20image%2020240420100056.png)
Luego de revisar los distintos directorios no encontramos nada util, asi que nos concentramos nuevamente en la version del servicio en ejecucion IIS 6.0 de la cual encontramos un exploit que nos permite ejecucion remota de comandos gracias a un buffer overflow.
https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269/blob/master/iis6%20reverse%20shell
Asi que preparamos nuestro exploit y seteamos un listener dentro de metasploit con el multi handler.
![](../../Images/Pasted%20image%2020240420101526.png)
![](../../Images/Pasted%20image%2020240420101546.png)
![](../../Images/Pasted%20image%2020240420101557.png)
Unos segundos luego de ejecutarlo recibimos nuestro revshell en metasploit.
![](../../Images/Pasted%20image%2020240420101929.png)
Ahora que tenemos nuestra sesion la ponemos en segundo plano y podemos utilizar el modulo local_exploit_suggester para verificar posibles caminos disponibles para escalar nuestros privilegios.
Al utilizarlo no nos trae nada, esto es porque no tenemos una sesion de meterpreter y al intentar actualizarla la misma falla, por lo que buscamos el exploit que utilizamos dentro de metasploit.


-------------------------------------------------------------------------------------

![](../../../Pasted%20image%2020240421130824.png)

