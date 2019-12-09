## Simple Mail Transfer Protocol

#### mail servers can also be used to gather information about a host or network
SMTP supports several important commands such as ***VRFY*** and ***EXPN***
***VRFY***: verify an email address
***EXPN***: asks the server for the membership of mailing list

#### EXAMPLE
###### nc -nv [victim_ip] [smtp_port]
- VRFY root
- VRFY [some_user_name]

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
connect=s.connect(('192.168.11.215',25))
banner=s.recv(1024)
print(banner)
s.send('VRFY'+sys.argv[1]+'\r\n')
result=s.recv(1024)
print(result)
s.close()
```
