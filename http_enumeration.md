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
###### only number 9 - SQL injection
- nikto -Tuning 9 -h [victim_ip]6
###### everything except number 6 - DOS
- nikto -Tuning x 6 -h [victim_ip]

##### Nmap scan
- Windows Machine
  - nmap -oN http.nmap –script "http and not http-brute and not http–brute and not http-slowloris and not http-rfi-spider and not http-sql-injectionand not http-form" –script-args= -d -sV –version-intensity 9 -Pn -vv -p 80 [victim_ip]
- Unix Machine
  - nmap -oN http.nmap –script “http and not http-brute and not http-slowloris and not http-rfi-spider and not http-sql-injection and not http-form and not http-iis*” –script-args= -d -sV -Pn -T3 -vv -p [victim_ip]
  
#### WhatWeb
**another enum type tool like nikto but looks to be more advanced and prettier in output**
- whatweb -v -a 4 http://[victim_ip]

