### SNMP

#### SNMP Enumeration

SNMP is based on UDP, a simple, stateless protocol, and therefore susceptible to IP spoofing and replay attacks. SNMP information and credentials can be easily intercepted over a local network.

#### MIB Tree

SNMP Managment Information Base (MIB) is a database contains info related to network management. 

#### Scanning for SNMP
- nmap -sU --open -p 161, [victim_ip] 

#### Windows SNMP Enumeration Example
 - snmpwalk -c public v1 [victim_ip]
 - snmpget
 
 // todo more examples
 

