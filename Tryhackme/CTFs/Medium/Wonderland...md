![[Pasted image 20231029004802.png]]

Abrimos nuestra maquina virtual e iniciamos nuestro VPN mientras el ctf se inicia.
Una vez iniciada mientras lanzamos un ping a la IP objetivo creamos una carpeta con el nombre de la maquina (con en fin de mantener un orden en nuestra VM).
![[Pasted image 20231029005942.png]]
Ya que el ping fue exitoso podemos realizar un escaneo con nmap de forma tradicional y mientras tanto verificamos si buscando la direccion ip del objetivo en la web encontramos algo.
![[Pasted image 20231029010144.png]]
Ya que encontramos ponernos a correr un dirb en la pagina para verificar si encontramos subdominios.
Mientras realizábamos estas tareas nuestro escaneo con nmap finalizo y en el encontramos tanto un puerto 80 como el puerto 22 (ssh) abiertos.
![[Pasted image 20231029010344.png]]
De todas formas correremos un escaneo de puertos mucho mas exhaustivo a continuación.
Revisando el código fuente de la web encontramos una carpeta llamada img.
![[Pasted image 20231029010621.png]]
Si navegamos hacia ella encontramos 3 imágenes mas.
![[Pasted image 20231029010700.png]]
El segundo escaneo con nmap no arrojo nuevos resultados.
Ya que dirb estaba tardando demasiado
![[Pasted image 20231029011807.png]]
Pase a utilizar gobuster con una lista de sectist
![[Pasted image 20231029011850.png]]
Se encontraron 3 directorios así que revisaremos primero poem y luego r.
El primero parece ser efectivamente un poema
![[Pasted image 20231029012017.png]]
El segundo con un mensaje
![[Pasted image 20231029012049.png]]
Realizamos un gobuster sobre el directorio r y encontramos un subdir a.
![[Pasted image 20231029012133.png]]
![[Pasted image 20231029012208.png]]
Realizamos nuevamente un gobuster sobre el directorio reciente y todo parece indicar que los directorios conforman la palabra rabbit.
![[Pasted image 20231029012341.png]]
Si analizamos su código fuente parece haber unas credenciales alli.
![[Pasted image 20231029012603.png]]
Intentamos conectarnos por medio de SSH.
![[Pasted image 20231029012712.png]]
Efectivamente pudimos conectarnos por medio de ssh, ahora intentamos capturar la flag del usuario.
Vemos que en el home de alice se encuentra la flag de root, así que podemos intentar capturar la flag de alice en el directorio root.
![[Pasted image 20231029013438.png]]
Luego de algunos intentos fallidos encontramos la flag
![[Pasted image 20231029013634.png]]
Dentro del home de alice tambien se encuentra un script en python que puede ser ejecutado como el usuario rabbit, al revisarlo vemos que utiliza una libreria llamada "random" tal ves si logramos manipularla podemos obtener acceso al usuario rabbit.
![[Pasted image 20231029013955.png]]
Si lanzamos el script como el user rabbit:
![[Pasted image 20231029014044.png]]
Ahora somos ese usuario. Si vemos dentro de su home encontramos un archivo que parece estar ejecutando dos comandos:
![[Pasted image 20231029014702.png]]
Si podemos modificar el comando date podemos obtener el acceso de otro usuario. Para lo que en primer lugar agregamos el directorio tmp al PATH (ya que cuando un comando se ejecuta, tmp es en el primer lugar en el que se busca el comando). Teniendo en cuenta que el comando del script no tiene una ruta especificada, el comando se buscara primero en el PATH.
![[Pasted image 20231029014927.png]]
Ahora tenemos tmp en el primer lugar:
![[Pasted image 20231029014948.png]]
Una vez creado nuestro date
![[Pasted image 20231029015151.png]]
Probamos a ejecutar el script en el home de rabbit.
![[Pasted image 20231029015258.png]]
Ahora somo hatter, así que revisamos su home
![[Pasted image 20231029015334.png]]
Si revisamos el archivo encontramos una contraseña.
![[Pasted image 20231029015353.png]]
Sabiendo eso podemos loguearnos por ssh con este nuevo usuario.
Una vez logueados intentamos escalar los privilegios a root, para ello intentamos buscar con
- sudo -l
- find / -type -f -perm -04000 -ls 2>/dev/null
- y con las capabilities: getcap -r / 2>/dev/null
Vemos que perl tiene las capabilities de suid, así que verificamos en gtfobins si podemos escalar con perl.
![[Pasted image 20231029021307.png]]
![[Pasted image 20231029021318.png]]
Efectivamente, probamos el comando de perl para escalar.
![[Pasted image 20231029021446.png]]
Funciono así que volvemos a la carpeta alice para obtener la ultima flag.