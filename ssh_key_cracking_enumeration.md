# Cracking encrypted private key

#### 1 ssh2john
```
ssh2john.py encrypted_private_key > private_key.john
```
#### 2 john
```
john private_key.john --wordlist=/usr/share/wordlists/rockyou.txt
```

#### tools:
- https://github.com/openwall/john/blob/bleeding-jumbo/run/ssh2john.py
