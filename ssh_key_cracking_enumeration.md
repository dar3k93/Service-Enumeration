# Cracking encrypted private key

### 1
```
ssh2john.py encrypted_private_key > private_key.john
```

### 2
```
john private_key.john --wordlist=/usr/share/wordlists/rockyou.txt
```
