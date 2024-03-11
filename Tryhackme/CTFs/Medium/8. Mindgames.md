![](../../Images/Pasted%20image%2020231127184501.png)

Realizamos un primer escaneo
![](../../Images/Pasted%20image%2020231127185134.png)
Verificamos la versión de servicios en esos puertos
![](../../Images/Pasted%20image%2020231127185152.png)
Revisando la pagina web vemos que tenemos dos códigos de ejemplo codificados en brainfuck y tambien un campo de input (configurado como un form) que ejecutara el código que coloquemos
![](../../Images/Pasted%20image%2020231127185540.png)
Asi que utilizamos un payload de python para obtener un reverse shell, pasándolo primero por una codificación en brainfuck
![](../../Images/Pasted%20image%2020231127185848.png)
Luego de codificarlo y correrlo obtenemos nuestro revshell
![](../../Images/Pasted%20image%2020231127185909.png)
Luego de estabilizar la terminal obtenemos la flag del usuario
![](../../Images/Pasted%20image%2020231127190334.png)
Revisamos si la maquina tiene pkexec
![](../../Images/Pasted%20image%2020231127190406.png)
Al tener pkexec hacemos uso del CVE-2021-4034 descargándolo a nuestra maquina atacante, activando un servidor http con python para descargar el exploit con la maquina victima a su /tmp.
![](../../Images/Pasted%20image%2020231127190726.png)
![](../../Images/Pasted%20image%2020231127190738.png)
Una vez descargado lo ejecutamos y obtenemos nuestro root shell
![](../../Images/Pasted%20image%2020231127190757.png)
![](../../Images/Pasted%20image%2020231127190804.png)
