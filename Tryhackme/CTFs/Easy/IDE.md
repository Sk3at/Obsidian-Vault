![[Pasted image 20231109180433.png]]
Un primer escaneo agresivo con nmap nos muestra que tenemos 4 puertos abiertos:
![[Pasted image 20231109182347.png]]
Vamos a realizar ahora un scan sobre esos puertos para ver la versión de los servicios que están en ejecución.
![[Pasted image 20231109182750.png]]
Tenemos una sesión ftp, un ssh y dos servidores web apache. 
Comenzamos revisando si el ftp tiene el anonymous login habilitado.
![[Pasted image 20231109182951.png]]
Tiene habilitada la entrada como anon y vemos tambien un directorio ...
![[Pasted image 20231109183044.png]]
Al ingresar al directorio vemos un archivo llamado -
Asi que lo descargamos a nuestra local.
![[Pasted image 20231109183209.png]]
El archivo contiene dos nombres de usuario john y drac además nos habla de una imagen y de que john tiene la contraseña por defecto (aunque no sabemos de que servicio).
Ahora nos dirigimos al navegador web y revisamos primero el puerto 80
![[Pasted image 20231109183345.png]]
Al revisar el código fuente no encontramos nada que no llame la atención, así que procedemos a realizar un gobuster sobre esta pagina (puerto 80) utilizamos los diccionarios common y big y no encontramos nada.
Asi que ahora probamos sobre la web que se encuentra en el puerto 62337
![[Pasted image 20231109183734.png]]
Encontramos un panel de login en el que probablemente el usuario john tenga las credenciales por defecto, así que probamos con la contraseña password y estamos dentro.
![[Pasted image 20231109184421.png]]
Buscamos en el navegador codiad exploit y el primer resultado es un RCE en exploit-db asociado al CVE 2018-14009, asi que revisamos su codigo para tener una nocion de como funciona.
![[Pasted image 20231109184627.png]]
Al descargarlo debemos configurar el usuario de autenticacion de codiad
![[Pasted image 20231109184659.png]]
Asi que procedemos a descargarlo y darle permisos de ejecucion
![[Pasted image 20231109184939.png]]
Intentamos ejecutarlo para obtener una vista de su modo de uso.
![[Pasted image 20231109184959.png]]
Lanzamos el comando con las opciones necesarias
![[Pasted image 20231109190003.png]]
Este para ejecutar el payload nos pide que pongamos a disposición 2 listeners
![[Pasted image 20231109190028.png]]
![[Pasted image 20231109190038.png]]
En el segundo es que la maquina se conecta, así que estando dentro confirmamos nuestro usuario.
![[Pasted image 20231109190108.png]]
Ahora intentamos escalar privilegios con las distintas técnicas.
Intentamos con las 3 formas que conocemos y no encontramos ningún binario, cap o suid que nos sirva.
Al no encontrar nada útil vamos a revisar los directorios
![[Pasted image 20231109190745.png]]
Al revisar en el historial de bash del único usuario que tiene home vemos lo que parecieran ser credenciales de inicio de sesión, las vamos a probar en el ssh que tiene la victima.
![[Pasted image 20231109190933.png]]
Estamos dentro como el usuario drac así que podemos ahora revisar nuevamente los binarios y permisos para escalar privilegios.
Nuevamente no encontramos ninguna manera para escalar con estos métodos, pero al realizar el comando pkexec vemos que la maquina lo tiene instalado, por lo que nos descargamos el exploit relacionado al CVE-2021-4034 (copiamos el código y lo pegamos en un archivo que creamos en la victima).
![[Pasted image 20231109192710.png]]
Al código una vez copiado le dimos los permisos de ejecución
![[Pasted image 20231109192736.png]]
Y lo ejecutamos
![[Pasted image 20231109192747.png]]
De forma que escalamos los privilegios y ahora somos root, por lo que realizamos la búsqueda de ambas flags.
![[Pasted image 20231109193025.png]]




