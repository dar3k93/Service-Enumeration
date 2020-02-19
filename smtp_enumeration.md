## Simple Mail Transfer Protocol

#### mail servers can also be used to gather information about a host or network
SMTP supports several important commands such as ***VRFY*** and ***EXPN***
***VRFY***: verify an email address
***EXPN***: asks the server for the membership of mailing list

###### nc -nv [victim_ip] [smtp_port]
- VRFY root
- VRFY [some_user_name]

##### telnet <victim_ip> <port>
 
##### Metasploit
- auxiliary/scanner/smtp/smtp_enum
  - set rhosts <victim_ip>
  - run

##### smtp-user-enum
- perl smtp-user-enum -M VRFY -U user.txt -t <victim_ip>

##### nmap enumeration
- nmap –script smtp-enum-users.nse <victim_ip>

###### example python VRFY automation script 
```python
#!/usr/bin/python
import socket
import sys
if len(sys.argv) != 2:
  print("Usage: vrfy.py [username]"):
  sys.exit(0)
s=socket.socket(socket.AF_INET,

socket.SOCK_STREAM)
connect=s.connect(('[victim_ip]',25))
banner=s.recv(1024)
print(banner)
s.send('VRFY'+sys.argv[1]+'\r\n')
result=s.recv(1024)
print(result)
s.close()
```
