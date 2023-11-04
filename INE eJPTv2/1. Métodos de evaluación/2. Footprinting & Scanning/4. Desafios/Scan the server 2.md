El objetivo de este desafío es:
- Identificar el puerto que utiliza el servicio Bind DNS
- Identificar el puerto que utiliza el servicio TFTP
- Identificar el puerto que utiliza el servicio SNMP

Se nos indica que la direccion IP del objetivo es un numero de host mas alto que el de nuestra direccion IP.

Solución:
En primer lugar utilizamos el comando ip add para identificar nuestra direccion IP:
![[Pasted image 20230919210146.png]]
Nuestra direccion IP es 192.69.104.2 por ende la direccion IP de nuestro objetivo es la 192.69.104.3
Procedemos a realizar un ping para verificar si se encuentra activo:
![[Pasted image 20230919210327.png]]
Procedemos a realizar el primer escaneo con nmap:
![[Pasted image 20230919210420.png]]
Vemos que no obtenemos respuesta, por lo que vamos a escanear todos los puertos disponibles con algunas opciones para hacerlo "mas veloz":
![[Pasted image 20230919210601.png]]
Vemos que para TCP solo encontramos un puerto abierto, verificamos que servicio corre en el mismo:
![[Pasted image 20230919210737.png]]
Vemos que se encuentra corriendo un Bind en ese puerto. 

El siguiente paso es verificar si tenemos puertos UDP abiertos, por lo que agregamos a nmap la opción -sU. Ya que el escaneo de puertos UDP demora bastante vamos a limitar el escaneo de puertos a 250 con el comando -p 1-250 y si obtenemos resultados realizaremos un escaneo mas exhaustivo sobre el resultado:
![[Pasted image 20230919212130.png]]
Vemos 3 puertos udp habilitados, el 134, 177 y 234. Por lo que en nuestro próximo escaneo nos concentraremos en estos 3 puertos para tratar de averiguar que servicios corren en ellos:
![[Pasted image 20230919212553.png]]
Con nuestro ultimo escaneo logramos identificar el servicio SNMP en el puerto 234 y el servicio DNS en el puerto 177, pero no logramos identificar que servicio se esta ejecutando en el puerto 134.
Podemos suponer que en ese puerto se ejecuta TFTP, comprobemos si es correcto:
![[Pasted image 20230919213223.png]]
Para conectarnos mediante tftp debemos emitir el comando:
**tftp host puerto**
Una vez dentro podemos ver los comandos disponibles con **?** 
Tambien podemos ver si la conexión se realizo de forma correcta con **status**
Por ultimo podemos salir con el comando **quit**

Conclusion:
- Identificar el puerto que utiliza el servicio Bind DNS
- Identificar el puerto que utiliza el servicio TFTP
- Identificar el puerto que utiliza el servicio SNMP


_____________________________________________________________
El protocolo trivial de transferencia de archivos (TFTP) es un protocolo simple que proporciona una función básica de transferencia de archivos sin autenticación de usuario.


