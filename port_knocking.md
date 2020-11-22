
# Port knocking configuration file
```
/etc/knocked.conf
```
**squence** value its sequence of ports someone must access to open or close port.

## Port knocking example with bash script
```
for i in 7 2350 43;
  do nmap -Pn -p $i --host-timeout 201 --max-retries 0 [victim_ip]; 
done
```

## Port knocking example with nmap scan
```
nmap -Pn -p $i --host-timeout 100 --max-retries 0 [victim_ip]; 
```

## Port knocking example with hping
```
hping3 -S [victim_ip] -p 1 -c 1
```
