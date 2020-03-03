### DNS
Is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet

#### Interacting with a DNS Server
- host -t ns [victim_domain]
- host -t mx [victim_domain]
###### By default every configured domain should provide at least the DNS and mail servers responsible for the domain

#### nslookup

-nslookup
-SERVER [victim_ip]
-127.0.0.1
and a name should be servername

#### dig
- dig axfr [victim_servername] @[victim_ip]

#### firece 
- firece -dns [victim_domain]

#### modify hosts file
- nano /etc/hosts
  ***syntax***
    [victim ip] [victim servername]

#### find email servers
- host -t mx [victim_ip]

#### use resolv.conf
- nano /etc/resolv.conf
  ***syntax***
    nameserver <victim_ip>
    
#### DNS enumeration (autoscan)
###### DNSrecon
 - dnsrecon -d [victim_scan] -t axfr

###### DNSEnum
- dnsenum [victim_scan]

#### zone transfer
- host -l [victim_ip] ns1.[victim_ip]
- dnsrecon -d [victim_scan] -t axfr

