
### Port knockd configure file
- /etc/knocked.conf
**squence** value its sequence of ports someone must access to open or close port.

#### example port koncking bash script
```
for i in 7 2350 43;
  do nmap -Pn -p $i --host-timeout 201 --max-retries 0 [victim_ip]; 
done
```

#### nmap port knocking
```
nmap -Pn -p $i --host-timeout 100 --max-retries 0 [victim_ip]; 
```

#### hping port knocking
```
hping3 -S [victim_ip] -p 1 -c 1
```
