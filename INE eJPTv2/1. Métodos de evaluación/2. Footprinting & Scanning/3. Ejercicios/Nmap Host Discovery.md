 Se nos provee una maquina Kali y una maquina objetivo. La maquina objetivo esta utilizando un firewall de Windows. Nuestra tarea es descubrir si el host esta disponible, que puertos están abiertos y que servicios y aplicaciones corren en él.

Nuestras instrucciones son:
- Descubrir la IP de nuestra maquina Kali. (Comienza con 10.10.X.X)
- La direccion IP de nuestro objetivo se encuentra en /root/Desktop/target.
- Descubrir el sistema operativo, puertos y servicios de la maquina objetivo.

Solución:
En primer lugar abrimos una nueva terminal en nuestro Kali y emitimos el comando para verificar la direccion IP de nuestra maquina:
**ip add | grep "10.10. \*"**
![[Pasted image 20230919022604.png]]
Como se puede observar la dirección IP de nuestro Kali es la 10.10.23.5 con una mascara de subred 255.255.255.0

Ahora procedemos a ubicar la direccion de nuestra maquina objetivo guardada en /root/Desktop/target. Para ello vamos a utilizar el comando:
**cat /root/Desktop/target**
![[Pasted image 20230919023059.png]]
La direccion IP de nuestro objetivo es la 10.4.26.55

Procedemos a realizar un ping a la maquina objetivo para verificar si la misma responde a las solicitudes ICMP:
![[Pasted image 20230919023250.png]]
Como se puede observar la maquina no responde a nuestra solicitud, esto puede ser o porque el host no se encuentra activo o bien porque esta configurado para no responder.

Lo que haremos a continuación es realizar un nmap por defecto pero con la opción -Pn para verificar si podemos ver algún puerto de la maquina, el comando se ve de la siguiente manera:
**nmap -Pn 10.4.26.55**
![[Pasted image 20230919023556.png]]
Luego de este primer escaneo podemos asegurar que el host se encuentra disponible y hay varios puertos abiertos en el mismo. Ahora que sabemos esto podemos ser un poco mas precisos con nuestro próximo escaneo listando los servicios que corren en cada puerto, la versión e incluso el sistema operativo del host. Para ello vamos a utilizar el comando:
**nmap -sV -sC -O -Pn 10.4.26.55**
![[Pasted image 20230919024304.png]]

Respuestas:
- IP Kali: 10.10.23.5/24
- IP Objetivo: 10.4.26.55
	- S.O: Windows Server 2009 R2 - 2012
	- Puertos
		- 80: http
		- 135: msrpc
		- 139: netbios-ssn
		- 445: microsoft-ds
		- 3389: ssl/ms-wbt-server
		- 49154: msrpc
		- 49155: msrpc
		- 49167: msrpc