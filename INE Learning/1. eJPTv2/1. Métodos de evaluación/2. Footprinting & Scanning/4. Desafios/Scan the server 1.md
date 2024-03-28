El objetivo de este desafío es realizar un escaneo de puertos y detección de servicios con nmap. 

Solución:
Primero utilizamos el comando ip add para verificar el ip de nuestro host:
![[../../../Images/Pasted image 20230919195421.png]]
Se nos provee la direccion objetivo como 192.169.197.3 por lo que realizamos un ping al host para saber si esta disponible:
![[../../../Images/Pasted image 20230919195511.png]]
Vemos que el mismo responde a la solicitud de ping.
Ahora realizamos un escaneo con nmap del host:
![[../../../Images/Pasted image 20230919195616.png]]
Observamos que no encontramos puertos abiertos en los 1000 puertos mas utilizados, por lo que ampliamos el escaneo de puertos a todos los puertos disponibles agregando -p-:
![[../../../Images/Pasted image 20230919195733.png]]
Con este ultimo escaneo vemos que se encuentran los siguientes puertos abiertos corriendo estos servicios:
PORT       STATE    SERVICE        VERSION
6421         open    mongodb      MongoDB 2.6.10
41288       open    memcached  Memcached
55413       open    ftp                 vsftpd 3.0.3