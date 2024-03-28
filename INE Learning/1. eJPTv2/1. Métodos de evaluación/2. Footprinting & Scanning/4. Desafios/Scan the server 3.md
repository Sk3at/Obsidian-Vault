Nuestro objetivo es encontrar puertos y servicios en el host.

Primero identificamos nuestra ip con ip add
![[../../../Images/Pasted image 20230919222049.png]]
Nuestra maquina objetivo es la 192.51.142.3
![[../../../Images/Pasted image 20230919222212.png]]
Verificamos que se encuentra activa.
Ahora comenzamos con los escaneos:
![[../../../Images/Pasted image 20230919222415.png]]
En el escaneo completo de puertos TCP no encontramos ninguno abierto, realizamos el escaneo común de puertos UDP:
![[../../../Images/Pasted image 20230919230216.png]]
Vemos que se encuentra abierto el puerto udp 161 por lo que realizamos un escaneo mas profundo sobre el mismo:
![[../../../Images/Pasted image 20230919230353.png]]
Con este ultimo escaneo podemos ver que se encuentra en funcionamiento el servicio snmp y que las claves ssh del usuario David se encuentran en /opt/david_key