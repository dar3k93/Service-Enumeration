### Oracle

#### 1521
***tool*** https://tools.kali.org/vulnerability-analysis/tnscmd10g
- tnscmd10g version -h [victim_ip]
- tnscmd10g status -h [vitcim_ip]
 
##### usefull tools set
- https://www.oracle.com/pl/database/technologies/instant-client/winx64-64-downloads.html

- Identify SIDs
```
odat sidguesser -s <victim_ip>
```
### default credentials
scott:trger

Check databae
```
sqlplus SCOTT/tiger@10.10.10.82:1521/<XE> depends SID
```

db PrivEsc
```
SQL> select * from user_role_privs;
```

check  privs with sysdba 
```
SQL> sqlplus SCOTT/tiger@10.10.10.82:1521/XE as sysdba
```

check for upload permission
```

```
#TO DO

#### 2100
```
credentials:
sys:sys
scott:trger
```

### resources
- https://www.blackhat.com/presentations/bh-usa-09/GATES/BHUSA09-Gates-OracleMetasploit-SLIDES.pdf
