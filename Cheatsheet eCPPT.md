INFO-GATHER
whois [DOMINIO] > para la shell
www.who.is º > para consultar en la web.
host [DOMINO] > para ver direcciones IP
dnsrecon -d [WEB] > ver registros DNS

SCAN TARGET
FASTSCAN: nmap -p- --open -sS -n -Pn --min-rate 5000 $target

SMB
smbexec.py 'username:password'@IP > se conecta al objetivo
smbclient -L [HOST] -N > listar shares sin pasar contraseña
smbclient -N //[HOST]/[SHARE] > nos conectamos al share sin pasar contraseña

EMPIRE POWERSHELL
powershell-empire server > inicia el servidor de empire
powershell-empire client > inicia el cliente

LOOT/POSTEXPLO
printenv > imprime las variables de entorno

