### HTTP enumeration

##### Directory scanning
- dir mode
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt
- dns mode
  - gobuster dns -d 10.11.1.x -w ~/wordlists/subdomains.txt
  - gobuster dns -d google.com -w ~/wordlists/subdomains.txt -i (with ip)
- extension usage
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -x .php, .txt, .html
- string usage
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -s "200"
- expanded usage(show full url)
  - gobuster -e dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt
- useragent usage
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -a CustomAgent
- export options
  - gobuster dir -u https://10.10.1.x -w ~/wordlists/shortlist.txt -o output.txt
- proxy chain
  -  gobuster -o gobuster.txt -e -u http://10.11.1.x/ -w ~/wordlist/shortlist.txt
  

##### Nikto scan
- nikto -h [victim_ip]
- nikto -Display V -h [victim_ip]
- nikto -Display V -o results.html -Format htm -h [victim_ip]
```
0 – File Upload
1 – Interesting File / Seen in logs
2 – Misconfiguration / Default File
3 – Information Disclosure
4 – Injection (XSS/Script/HTML)
5 – Remote File Retrieval – Inside Web Root
6 – Denial of Service
7 – Remote File Retrieval – Server Wide
8 – Command Execution / Remote Shell
9 – SQL Injection
a – Authentication Bypass
b – Software Identification
c – Remote Source Inclusion
x – Reverse Tuning Options (i.e., include all except specified)
```
###### Only number 9 - SQL injection
```
nikto -Tuning 9 -h [victim_ip]6
```

###### Everything except number 6 - DOS
```
nikto -Tuning x 6 -h [victim_ip]
```

#### WhatWeb
**Another enum type tool like nikto but looks to be more advanced and prettier in output**
- whatweb -v -a 4 http://[victim_ip]

#### Cewl
- create dict via https://tools.kali.org/password-attacks/cewl and use as dirb list scan

