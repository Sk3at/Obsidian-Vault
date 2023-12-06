![](../../Images/Pasted%20image%2020231205114848.png)
Comenzamos realizando un escaneo de la maquina con nmap para verificar puertos abiertos.
![](../../Images/Pasted%20image%2020231205115209.png)
Ahora realizamos un escaneo un poco mas especifico sobre los puertos que encontramos abiertos.
![](../../Images/Pasted%20image%2020231205115456.png)
Vemos que tenemos ssh, un servidor web y un ftp que permite el login anonymous.
Dentro del servidor FTP vemos un directorio que contiene una nota para Mitch así que la pasamos a nuestra maquina atacante.
![](../../Images/Pasted%20image%2020231205115746.png)
En la nota vemos lo siguiente
![](../../Images/Pasted%20image%2020231205115813.png)
Se esta utilizando una contraseña débil y esa misma contraseña esta siendo utilizada en el sistema.
Por lo que nos tomamos un momento para revisar la web, tanto su código fuente como lanzando un ataque de fuerza bruta sobre este con gobuster.
![](../../Images/Pasted%20image%2020231205120019.png)
Vemos dos directorios interesantes, simple y robots, primero revisamos el robots y no encontramos nada, por lo que nos dirigimos al directorio simple, el cual se trata de un CMS, revisando un poco la pagina encontramos la versión de CMS que se encuentra en uso.
![](../../Images/Pasted%20image%2020231205120155.png)
Buscamos con searchsploit si encontramos algún exploit contra esta versión de servicio y vemos que es vulnerable a sqli.
![](../../Images/Pasted%20image%2020231205120423.png)
Asi que copiamos el exploit en nuestro directorio actual para revisarlo.
![](../../Images/Pasted%20image%2020231205120531.png)
Vemos un ejemplo de su uso en el código del mismo
![](../../Images/Pasted%20image%2020231205120652.png)
El exploit no para de fallar, así que nos dirigimos a la web en busca de otro exploit que pueda ser de utilidad y nos topamos con un poc del  CVE-2019-9053 en https://github.com/Mahamedm/CVE-2019-9053-Exploit-Python-3 así que lo descargamos e intentamos ejecutarlo (el código es muy similar al exploit anterior, solo que tiene algunos cambios).
![](../../Images/Pasted%20image%2020231205122624.png)
Luego de ejecutarlo el exploit comienza a funcionar realizando distintas pruebas hasta llegar a los resultados luego de unos minutos. 
Dentro de las pistas de THM vemos lo siguiente
![](../../Images/Pasted%20image%2020231205123043.png)
Por lo que decidimos cancelar la ejecución del comando y probar el diccionario sugerido.
![](../../Images/Pasted%20image%2020231205123127.png)




