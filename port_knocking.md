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

### Port konckd configure file
```
sudo vi /etc/knockd.conf

squence: for example 700,600,5000
its sequence of ports someone must access to open or close port ???
```
