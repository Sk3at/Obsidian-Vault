![[Pasted image 20231112175317.png]]
Un primer escaneo con nmap nos muestra tres puertos abiertos
![[Pasted image 20231112175807.png]]
Ahora realizamos un escaneo de puertos mas profundo para verificar versiones
![[Pasted image 20231112180347.png]]
Nos dirigimos a la pagina web en donde encontramos la primera respuesta (el team).
![[Pasted image 20231112180545.png]]
El hipervínculo nos dirige hacia un directorio /mansionmain/ en el que se nos pregunta donde esta la habitación.
![[Pasted image 20231112180723.png]]
Revisamos su código fuente y...
![[Pasted image 20231112181057.png]]
Revisamos ese directorio pero antes ponemos a correr un gobuster de la pagina principal para listar otros posibles directorios.
![[Pasted image 20231112181202.png]]
Vemos algunos resultados de los que tomamos nota y realizamos una nueva enumeración de  /mansionmain/ donde no encotramos nada, asi que nos dirigimos a la web y abrimos la /diningRoom/
![[Pasted image 20231112181708.png]]
Encontramos un emblema
![[Pasted image 20231112181729.png]]
Al revisar el código fuente dentro de dinnigRoom vemos lo siguiente
![[Pasted image 20231112182959.png]]
Un código que podría ser un mensaje, al revisarlo en dcode vemos que es un base 64 y su mensaje
![[Pasted image 20231112183047.png]]
Asi que nos dirigimos alli
![[Pasted image 20231112183127.png]]
Se nos da un lockpick y se nos dice que debemos visitar la /artRoom/ en donde encontramos
![[Pasted image 20231112183244.png]]
![[Pasted image 20231112183311.png]]
Un mapa, así que comenzamos revisando las localizaciones que nos falta
En la barRoom podemos utilizar el lockpick
![[Pasted image 20231112183414.png]]
Una vez utilizado se abre la puerta hacia el bar donde se ve un piano y una nota
![[Pasted image 20231112183545.png]]
La misma esta codificada en base32, al decodificarla obtenemos la nota musical para el piano.
![[Pasted image 20231112183641.png]]
Al tocarla en el piano encontramos un emblema
![[Pasted image 20231112183741.png]]
Al colocar el primer emblema en el espacio que dejo el dorado se nos da un nombre
![[Pasted image 20231112183948.png]]
Al utilizar el emblema dorado en la /dinningRoom/ vemos lo siguiente:
![[Pasted image 20231112184050.png]]
Realizamos la decodificacion en cyberchef y utilizamos el nombre rebecca
![[Pasted image 20231112185725.png]]
![[Pasted image 20231112185827.png]]
Dentro de la dinngRoom2F encontramos el camino a la gema azul
![[Pasted image 20231112184933.png]]
![[Pasted image 20231112184945.png]]
![[Pasted image 20231112185003.png]]
Nos dirigimos a la galleryRoom y encontramos en su codigo fuente el crest2
![[Pasted image 20231112185145.png]]
Ahora que tenemos el escudo nos dirigimos al attic donde conseguimos el crest 4
![[Pasted image 20231112190013.png]]
En el armorroom se nos pide el simbolo del escudo
![[Pasted image 20231112190120.png]]

Encontramos el tercer crest
![[Pasted image 20231112190218.png]]
En la tigerRoom si utilizamos la gema azul vemos el crest 1
![[Pasted image 20231112191039.png]]
El crest 1 resulta estar codificado primero en 64 y luego en 32, su resultado es RlRQIHVzZXI6IG
El crest 2 esta codificado en 32 y luego en 58, su resultado h1bnRlciwgRlRQIHBh
El crest 3 los realizamos en Cyberchef desde base64 a binario a hexa y su resultado c3M6IHlvdV9jYW50X2h
![[Pasted image 20231112192835.png]]
El crest 4 se encuentra en base58 y en hex, su resultado es pZGVfZm9yZXZlcg==
Al realizar el decode de los 4 crest vemos las credenciales de ftp
![[Pasted image 20231112193205.png]]
Dentro del servidor ftp vemos varios archivos que descargamos de forma local
![[Pasted image 20231112193508.png]]
Revisamos los archivos comenzando por important.txt
![[Pasted image 20231112193555.png]]
Vemos que hay un /hidden_closet/ en la web asi que revisamos, en la misma se nos pide el simbolo del casco.
En code.save parece haber algo encriptado en pgp por lo que necesitamos la parafrase.
Asi que analizamos las imagenes utilizando las distintas herramientas
En la key1 con el comando steghide info encontramos que la misma traer un txt
![[Pasted image 20231112194623.png]]
Asi que lo extremos con esteghide extract -sf
![[Pasted image 20231112194725.png]]
Ahora analizamos la key2 y con exiftool encontramos un comentario
![[Pasted image 20231112194758.png]]
Al revisar la key3 con exiftool no encontramos nada, pero con la info de steghide vemos que hay un archivo oculto, aun asi sin la parafrase no nos lo extrae
![[Pasted image 20231112194948.png]]
Asi que vamos a utilizar binwalk -e para extraerlo
![[Pasted image 20231112195138.png]]
Al juntar las 3 keys y decodificarlas con base64 encontramos lo siguiente
plant42_can_be_destroy_with_vjolt
Si lo utilizamos como parafrase para decodificar gpg obtenemos la helmet key
![[Pasted image 20231112195506.png]]
Dentro del studyroom se nos descargara un archivo .tar.gz si lo descomprimimos vemos el usuario ssh
![[Pasted image 20231112200240.png]]
Y dentro de la room que se nos dio en ftp tenemos la contraseña ssh
![[Pasted image 20231112200330.png]]
Dentro del hidden closet tambien encontramos una nota
![[Pasted image 20231112200921.png]]
Con esta utilizamos la siguiente web para decodificar vigenere sin la key https://www.boxentriq.com/code-breaking/vigenere-cipher?source=post_page-----4c43fda578ed--------------------------------
![[Pasted image 20231112200901.png]]
Una vez nos conectamos con nuestras credenciales ssh listamos el contenido del home y vemos una carpeta .jailcell
![[Pasted image 20231112201127.png]]
Al revisar en ese directorio vemos un archivo de texto el cual parece ser la key del vigenere anterior
![[Pasted image 20231112201740.png]]
![[Pasted image 20231112201749.png]]
Probamos cambiar a weasker con esta contraseña y es exitoso, de forma que realizamos un sudo -l y vemos que weasker puede lanzar cualquier comando como root sin contraseña, por lo que hacemos sudo su y realizamos un cat de root.txt
![[Pasted image 20231112202601.png]]


