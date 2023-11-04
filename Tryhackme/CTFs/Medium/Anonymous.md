![[Pasted image 20231030120810.png]]

Realizamos un ping a la maquina para verificar si responde a nuestra solicitud.
![[Pasted image 20231030120844.png]]
Realizamos un escaneo con nmap
![[Pasted image 20231030122155.png]]
Probamos conectarnos directamente por ftp con el usuario anonymous para verificar su contenido.
![[Pasted image 20231030122750.png]]
Encontramos una carpeta llamada scripts en la cual teníamos disponibles 3 archivos que descargamos para trabajar de forma local.
Realizamos un cat de los archivos y vemos que clean.sh se trata de un script que se encarga de borrar los archivos temporales.
![[Pasted image 20231030123557.png]]
Sabiendo esto podemos modificar el script para que ejecute un reverse shell y subirlo nuevamente al servidor ftp.
Modificamos nuestro script 
![[Pasted image 20231030125207.png]]
Intentamos subirlo al servidor ftp.
![[Pasted image 20231030125245.png]]
Podemos verificar desde la web si el archivo se coloco correctamente, pero antes configuraremos el listener el cual luego de unos momentos recibe el reverse shell.
![[Pasted image 20231030125848.png]]
Obtenemos la flag de usuario
![[Pasted image 20231030130040.png]]
Ahora toca buscar algún archivo que tenga el suid.
![[Pasted image 20231030130906.png]]
Luego de ejecutar el comando vemos una larga lista y en ella encontramos /usr/bin/env así que buscamos en gtfobins si tenemos algún método para escalar a root.
![[Pasted image 20231030131015.png]]
![[Pasted image 20231030131107.png]]
Así que ejecutamos el comando:
![[Pasted image 20231030131146.png]]
Buscamos la flag de root.
![[Pasted image 20231030131224.png]]

![[Pasted image 20231030131831.png]]
