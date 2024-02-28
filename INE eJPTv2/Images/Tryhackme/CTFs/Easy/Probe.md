![[../../Images/Pasted image 20231113205221.png]]
Realizamos un primer escaneo para tomar contacto con la maquina y ver que puertos se encuentran abiertos
![[../../Images/Pasted image 20231113205408.png]]
Realizamos un escaneo mas especifico sobre los puertos abiertos
![[../../Images/Pasted image 20231113205856.png]]
Al realizar un -sVC sobre los servicio http vemos lo siguiente:
![[../../Images/Pasted image 20231113214953.png]]
Con lo que respondemos sobre el FQDN y su certificado SSL.
Realizamos un gobuster sobre la web que se encuentra en el puerto 1443 
![[../../Images/Pasted image 20231113215125.png]]
La opcion -k  desactiva el chequeo tls
Dentro de la web 1443 vemos la  PHP Extension Build y tambien podemos responder el software que se utiliza para la base de datos (phpmyadmin).
![[../../Images/Pasted image 20231113215605.png]]
Mientras tanto en nikto en el 9007
![[../../Images/Pasted image 20231113215640.png]]
Vemos que se encontró un wordpress
![[../../Images/Pasted image 20231113215738.png]]
Por lo que lanzamos un wpscan en esa url
![[../../Images/Pasted image 20231113215830.png]]
El cual nos arroja informacion sobre la versión de wordpress en uso, luego lanzamos uno nuevo para enumerar usuarios
![[../../Images/Pasted image 20231113215901.png]]
El cual nos devuelve el usuario de wp.
En el escaneo con nikto se realiza la prueba de vulnerabilidad de OSVDB-3092 y se nos devuelve que el archivo es license.txt