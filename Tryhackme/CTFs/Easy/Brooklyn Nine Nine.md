![[Pasted image 20231102123434.png]]

Comenzamos realizando un ping a la maquina para verificar si responde al protocolo ICMP.
![[Pasted image 20231102123821.png]]
Ahora realizamos un escaneo con nmap.
![[Pasted image 20231102124007.png]]
Mientras se realiza el escaneo nos dirigimos al navegador y colocamos la direccion para verificar si hay disponible un servicio web.
![[Pasted image 20231102124054.png]]
El mismo existe así que verificamos el código fuente de la pagina para ver si encontramos algo de interés.
![[Pasted image 20231102124133.png]]
Vemos que el código fuente nos habla son esteganografía, así que podemos descargar la imagen y verificar con stego si encontramos algo oculto en ella.
Antes de trabajar con la imagen revisamos nuestro escaneo con nmap
![[Pasted image 20231102124355.png]]
Vemos que tenemos un puerto 21 y 22 abiertos, así que realizamos nuevamente un escaneo pero sin sC.
![[Pasted image 20231102124433.png]]
Probamos en el puerto 21 si podemos ingresar como anon.
Al realizarlo encontramos un archivo de texto el cual descargamos
![[Pasted image 20231102125521.png]]
Si abrimos la nota:
![[Pasted image 20231102125552.png]]
Vemos que Amy le pide a Jake que cambie su contraseña porque es muy débil.
Así que intentamos encontrar la contraseña con hydra.
![[Pasted image 20231102131004.png]]
*Nota: al intentar realizar la enumeración de usuario con metasploit no encontraba al usuario  jake, pero reconocía los usuarios amy y root, de todas formas se intento conseguir la contraseña de jake.*
![[Pasted image 20231102131629.png]]
Una vez dentro de la maquina como el usuario jake procedemos a ejecutar sudo -l para verificar si disponemos de la ejecución de algún comando como root y encontramos que podemos utilizar el comando less así que lo buscamos en gtfobins.
![[Pasted image 20231102131751.png]]
Una vez realizamos los comandos verificamos que somos root
![[Pasted image 20231102132059.png]]
Buscamos la flag de usuario
![[Pasted image 20231102132134.png]]
Y luego la flag de root
![[Pasted image 20231102132147.png]]

![[Pasted image 20231102132406.png]]
