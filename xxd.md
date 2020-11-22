### Reverse Hex dump
```
- xxd -r hex_dump > new_file
- mv new_file new_file.bz2
- bzip2 -d new_file.bz2
- mv new_file new_file.gz
- gzip -d new_file.gz
- mv new_file new_file.bz2
- bzip2 -d new_file.bz2
- mv new_file new_file.tar
- tar xvf new_file.tar
- cat ....
```
