
What I did:
I checked which services were running on my system. I looked for unsafe or unnecessary services that should not be active.

What I found:  
- Telnet was running (this is unsafe).  
- FTP was available.  
- SSH allowed password login.  
- Root login was still allowed.

What I changed:  
I disabled Telnet because it is insecure.  
I wrote down the SSH problems to fix next week.

Commands I used:  

systemctl --type=service
sshd -T
netstat -tulpn
```

Notes:  
I will add screenshots later.



