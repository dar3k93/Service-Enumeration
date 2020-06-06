```
for i in 7 2350 43;
  do nmap -Pn -p $i --host-timeout 201 --max-retries 0 [victim_ip]; 
done
```

```
nmap -Pn -p $i --host-timeout 100 --max-retries 0 [victim_ip]; 
```

```
hping3 -S [victim_ip] -p 1 -c 1
```
