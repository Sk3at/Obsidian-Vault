Realizamos un ping a la maquina victima.
![[Pasted image 20231106114527.png]]
Realizamos un escaneo con nmap
![[Pasted image 20231106123354.png]]
Revisamos en el navegador web para confirmar si encontramos un servidor
![[Pasted image 20231106120732.png]]
Realizamos una enumeración en la web con gobuster.
![[Pasted image 20231106115353.png]]
Realizamos una nueva enumeración dentro de Joomla.
![[Pasted image 20231106120508.png]]
Encontramos un subdominio \_test
![[Pasted image 20231106120523.png]]
En ese subdominio se esta utilizando sar2html que parece ser vulnerable a RCE
![[Pasted image 20231106120423.png]]
Encontramos un archivo log.txt dentro del directorio de test y al realizarle un cat vemos las credenciales del usuario basterd
![[Pasted image 20231106120446.png]]
Nos conectamos mediante ssh
![[Pasted image 20231106121916.png]]
Una vez dentro vemos un script llamado backup que resulta tener las credeenciales de otro usuario del sistema.
![[Pasted image 20231106121932.png]]
Realizamos el cambio de usuario y dentro de su home encontramos la primera flag.
![[Pasted image 20231106121945.png]]
Revisamos si podemos escalar privilegios con algún binario que tenga el SUID
![[Pasted image 20231106121959.png]]
Encontramos que find tiene el SUID así que buscamos en gtfobins:
![[Pasted image 20231106122011.png]]
Una vez ejecutado no convertimos en root y obtenemos la flag.
![[Pasted image 20231106122028.png]]

