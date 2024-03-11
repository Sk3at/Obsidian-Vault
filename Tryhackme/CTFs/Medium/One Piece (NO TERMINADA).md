![](../../Images/Pasted%20image%2020231120013355.png)
Realizamos un escaneo con nmap para verificar puertos abiertos.
![](../../Images/Pasted%20image%2020231120013852.png)
Realizamos un segundo escaneo para verificar la versión de los servicios en ejecución
![](../../Images/Pasted%20image%2020231120014055.png)
Vemos 3 puertos abiertos, entre la informacion encontramos qeu ftp es vulnerable al login anonimo.
Asi que nos conectamos a ftp y realizamos un listado, en el se visualiza un archivo y una carpeta oculta, descargamos todo a nuestra maquina local.
![](../../Images/Pasted%20image%2020231120013824.png)
Al revisar los archivos encontramos en la imagen datos adjuntos, así que los extraemos
![](../../Images/Pasted%20image%2020231120014541.png)
![](../../Images/Pasted%20image%2020231120014728.png)
Al extraerlos notamos que están cifrados
Para continuar desde aquí aplicamos un poco de ingeniería social y encontramos en el git del creador del CTF un archivo (diccionario) llamado log pose (este en la serie es utilizado por los personajes para orientarse a destino)
![](../../Images/Pasted%20image%2020231127191452.png)
Al utilizar gobuster en un principio no encontramos nada, pero luego especificamos extensiones de archivos.
![](../../Images/Pasted%20image%2020231127193407.png)
![](../../Images/Pasted%20image%2020231127193447.png)
Al revisar el codigo fuente encontramos una imagen que parece tener un texto crifrado.
![](../../Images/Pasted%20image%2020231210164502.png)
![](../../Images/Pasted%20image%2020231210164510.png)
La primera parte se encuentra en hexa, al decifrarla vemos lo siguiente:
![](../../Images/Pasted%20image%2020231210164806.png)
