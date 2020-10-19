[Amazon S3](#Amazon S3)
[DNS](#DNS)
--------------------------------------------------------------------------------------------------------------------------------
#Amazon_s3

***Bucket is a logical unit of storage in Amazon Web Services (AWS) object storage service, Simple Storage Solution S3. 
Buckets are used to store objects, which consist of data and metadata that describes the data.***

### awscli install
- pip3 install awscli

### aws configue if we have data
- aws configure

### list aws bucket
- aws s3 ls s3://<victim_aws_bucket_name>

***with no creds***
- aws s3 ls s3://<victim_aws_bucket_name> --no-sign-request

### file upload 
- echo "test" >> file.txt
- aws s3 cp file.txt s3:<victim_aws_bucket_name>/file.txt 

***with no creds***
- aws s3 cp file.txt s3:<victim_aws_bucket_name>/file.txt  --no-sign-request

### file remove
- aws s3 rm file.txt s3:<victim_aws_bucket_name>/file.txt
  
***with no creds***
- aws s3 rm file.txt s3:<victim_aws_bucket_name>/file.txt  --no-sign-request

### bucket remove
- aws s3 rb file.txt s3:<victim_aws_bucket_name>

***with no creds***
- aws s3 rb file.txt s3:<victim_aws_bucket_name>  --no-sign-request

### bucket list recursive
- aws s3 cp s3://<victim_aws_bucket_name> . --recursive

***with no creds***
- aws s3 cp s3://<victim_aws_bucket_name> . --recursive --no-sign-request

***in this case, aws return stack trace with file to which we have not got access***
--------------------------------------------------------------------------------------------------------------------------------
#DNS

#### Identifying DNS Server
```
nmap -sC -sV -p 53 [victim_ip]
```

#### Interacting with a DNS Server
```
- host -t ns [victim_domain]
- host -t mx [victim_domain]
```
###### By default every configured domain should provide at least the DNS and mail servers responsible for the domain

#### nslookup
```
- nslookup
> SERVER [victim_ip]
> 127.0.0.1
variable name should be servername
````

#### conduct z zone transfer with dig tool
```
- dig axfr [victim_servername] @[victim_ip]
example: dig axfr cronos.htb @10.10.10.13
```

#### fierce Domain DNS scanner
```
flag dns:  The domain you would like scanned.
- fierce -dns [victim_domain]
```

#### modify hosts file
```
- nano /etc/hosts
  ***syntax***
    [victim ip] [victim servername]
```

#### modify resolv.conf file

#### Search for email servers
```
- host -t mx [victim_ip]
```

#### use resolv.conf
```
- nano /etc/resolv.conf
  ***syntax***
    nameserver <victim_ip>
```

#### DNS enumeration (autoscan)
###### DNSrecon
```
 - dnsrecon -d [victim_scan] -t axfr
```

###### DNSEnum
```
- dnsenum [victim_scan]
```

#### zone transfer
```
- host -l [victim_ip] ns1.[victim_ip]
- dnsrecon -d [victim_scan] -t axfr
```
