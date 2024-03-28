Zenmap es la versión con interfaz de usuario grafica (GUI) de nmap, generalmente se utiliza en maquinas windows. 
Se nos provee una VM con Windows Server 2012, nuestra tarea es descubrir todas las maquinas disponibles dentro de la misma red.

Nuestras instrucciones son:
- Verificar la direccion IP de nuestra maquina.
- Descubrir todos los hosts disponibles en la misma red.

Solución:
En primer lugar iniciamos la maquina, abrimos un powershell o cmd y ejecutamos el comando ipconfig para verificar nuestra direccion IP:
![[../../../Images/Pasted image 20230919140611.png]]
Como podemos observar nuestra direccion IP es 10.4.27.140 con una mascara de subred 255.255.240.0, por ende nuestra direccion IP es 

El siguiente paso es abrir zenmap y comenzar con el escaneo de red:
![[../../../Images/Pasted image 20230919140922.png]]
Dentro de la GUI de zenmap colocamos el objetivo y seleccionamos el tipo de scan que deseamos realizar dentro de los perfiles, tambien es posible modificar la linea de comando a nuestro antojo.
Lanzamos el escaneo y obtenemos los siguientes resultados:
![[../../../Images/Pasted image 20230919141133.png]]
Como se observa, la salida nos devuelve todos los hosts que están conectados en la misma red, tenemos distintas formas de visualizar esto, como por ejemplo seleccionando la vista de topología.
![[../../../Images/Pasted image 20230919141516.png]]
