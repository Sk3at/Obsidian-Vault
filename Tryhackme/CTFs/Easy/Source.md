![[Pasted image 20231109170654.png]]

Realizamos un primer escaneo de forma agresiva para verificar que puertos se encuentran abiertos
![[Pasted image 20231109173718.png]]
El resultado fue que el puerto 22 y el puerto 10000 están abiertos, así que realizamos un escaneo con enumeración de versión.
![[Pasted image 20231109173747.png]]
Buscamos dentro de metasploit webmin y encontramos varios módulos
![[Pasted image 20231109173941.png]]
Revisamos la info del modulo exploit/linux/http/webmin_backdoor y parece que no requiere autenticacion ademas que es compatible con la version de webmin que tiene corriendo nuestra victima.
![[Pasted image 20231109174355.png]]
![[Pasted image 20231109174406.png]]
Lo seleccionamos y configuramos tanto la direccion de RHOSTS como LHOST e intentamos correrlo
![[Pasted image 20231109175124.png]]
Vemos un error que dice debemos setear a verdadero el ForceExploit, así que lo configuraos y volemos a intentar correr el comando.
![[Pasted image 20231109175228.png]]
Nuevamente vemos un error que dice debemos setear ssl a verdadero.
Si consultamos en el navegado web la direccion del equipo victima con el puerto vemos lo siguiente:
![[Pasted image 20231109175622.png]]
El servidor web se encuentra corriendo en modo SSL.
Por lo que configuramos la opción en el modulo e intentamos correrlo nuevamente.
![[Pasted image 20231109175717.png]]
En esta oportunidad vemos que se creo una sesión y esta abierta, así que ejecutamos el comando whoami para verificar nuestro usuario actual.
![[Pasted image 20231109175759.png]]
Como somos root utilizamos el comando find para encontrar ambas flags y finalizar la maquina.

