WEEK 3 – Hardened Services 

What I did:
This week I focused on improving the firewall and monitoring the system. I checked which ports should stay open and which should be blocked.
What I changed:
- Set up the firewall (UFW or firewalld).  
- Allowed only important ports (like SSH).  
- Blocked all other ports.  
- Checked logs to make sure services were running safely.

Problems:
Some ports were still open because older services were running in the background.

How I fixed it:
I stopped the unused services and restarted the firewall rules.

Commands I used:
sudo ufw enable
sudo ufw allow 22
sudo ufw status
journalctl -xe
systemctl stop <service>

