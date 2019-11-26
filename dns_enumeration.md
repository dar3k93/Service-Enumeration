### DNS
Is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet

#### nmap

#### nslookup

-nslookup
-SERVER <victim ip>
-127.0.0.1
and a name should be servername

#### dig
- dig axfr <victim_servername> @<victim_ip>

#### modify hosts file
- nano /etc/hosts
  ***syntax***
    <victim ip> <victim servername>
    
#### use resolv.conf
- nano /etc/resolv.conf
  ***syntax***
    nameserver <victim_ip>
