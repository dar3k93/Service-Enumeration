- [port scan](#nmap)
- [heartbleed](#heartbleed)
- [vuln](#vuln)
- [smb](#smb)
- [shellshock](#shellshock)

### nmap port scan
```
nmap -p- --min-rate 10000 10.10.10.10
```

### heartbleed
```
nmap -p [victim_port] --script ssl-heartbleed [victim_ip]
```

### vuln
```
nmap -p [victim_port] --script vuln [victim_ip]
```

### smb
```
nmap -p [victim_port] -vv --script=smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse [victim_ip]
```

### shellshock
```
nmap --script -p [victim_port] http-shellshock --script-args uri=[/vuln/path] cmd=[yours_command] [victim_ip]
```
