### SMB:
  It's protocol for sharing files and resources. Runs on port 445 or on port 139
  
##### nmap:
- ls -la /usr/share/nmap/scripts/smb*
- nmap -v -p 139, 445 --scrip=smb-os-discovery [victim_ip]
- nmap -v -sSVC -p 139, 445 --script discovery [victim_ip]
- nmap --script smb-enum-shares -p 139,445 [victim_ip]
- nmap -p 445 -vv --script=smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse [victim_ip]
- nmap -p 445 -vv --script=smb-enum-shares.nse,smb-enum-users.nse [victim_ip]
- nmap -sV -p 139,445 --script=smb-vuln-* --script-args=unsafe=1 [victim_ip]

#### rpcclient
- rpcclient -U "" -N [victim_ip]
  -U "" - null session
  -N - no password

##### smbmap
  - smbmap -H <victim_ip>
  - smbmap -H <victim_ip> -R
  - smbmap -H <victim_ip> -u anonymous -d <directory>
  
  ***H***: hostname
  ***R***: recursive, go through each directory and oyt the files
  ***U***: username
  
#### smbclinet
  - smbclient -L [victim_ip]
  - smbclient \\\\[victim_ip]\\<directory>
  - smbclient -N -L \\\\\[victim_ip]
  
#### enum4linux
  - Share Enumeration:
    - enum4linux-S [victim_ip]
  - Usernames Enumeration:
    - enum4linux -U -P [victim_ip]
  - All Enumeration:  
    - enum4linux -a [victim_ip]
    
#### msfconsole
  - setg rhosts 192.168.55.248
  - use auxiliary/scanner/smb/smb_enumusers
    - run
  - use auxiliary/scanner/smb/smb_enumshares
    - run
  - use auxiliary/scanner/smb/smb_version
    - run
##### create a resource file
```
  echo 'setg rhosts 192.168.55.248' > smbscan.rc
  echo 'use auxiliary/scanner/smb/smb_enumusers' >> smbscan.rc
  echo 'run' >> smbscan.rc
  echo 'use auxiliary/scanner/smb/smb_enumshares' >> smbscan.rc
  echo 'run' >> smbscan.rc
  echo 'use auxiliary/scanner/smb/smb_version' >> smbscan.rc
  echo 'run' >> smbscan.rc
  
  msfconsole -r smbscan.rc
```

#### working with smb
  - file upload
  ***smb:> get "filename"***
  
#### Manual Inspection
```
if [ -z $1 ]; then echo "Usage: ./smbver.sh RHOST {RPORT}" && exit; else rhost=$1; fi
if [ ! -z $2 ]; then rport=$2; else rport=139; fi
tcpdump -s0 -n -i tap0 src $rhost and port $rport -A -c 7 2>/dev/null | grep -i "samba\|s.a.m" | tr -d '.' | grep -oP 'UnixSamba.*[0-9a-z]' | tr -d '\n' & echo -n "$rhost: " &
echo "exit" | smbclient -L $rhost 1>/dev/null 2>/dev/null
sleep 0.5 && echo ""
```
usage: ./script.sh [victim_ip]

#### Checklist
- Enumerate hostname: nmblookup -A [victim_ip]
- List shares
  - smbmap -H [victim_ip]
  - echo exit | smbclient -L \\\\[victim_ip]
  - nmap --script smb-enum-shares -p 139,445 [victim_ip]
- Check Null Sessions
  - smbmap -H [victim_ip]
  - rpcclient -U "" -N [victim_ip]
  - smbclient \\\\[victim_ip]\\[share name]
- Check for Vulnerabilities
  - nmap --script smb-vuln* -p 139,445 [victim_ip]
- Overall Scan: enum4linux -a [victim_ip]

### SMB 7.pl (usefull script)
- https://github.com/offensive-security/exploitdb/blob/master/exploits/linux/remote/7.pl

### references
- https://0xdf.gitlab.io/2018/12/02/pwk-notes-smb-enumeration-checklist-update1.html#nmap
