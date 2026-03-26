1. Bucket Operations

Create Bucket

aws s3 mb s3://my-bucket-name --region ap-south-1

List Buckets

aws s3 ls

Delete Bucket

aws s3 rb s3://my-bucket-name

Delete Bucket (force, with all objects)

aws s3 rb s3://my-bucket-name --force

2. Object Operations

Upload File

aws s3 cp file.txt s3://my-bucket-name/

Upload with specific storage class

aws s3 cp file.txt s3://my-bucket-name/ --storage-class STANDARD_IA

Download File

aws s3 cp s3://my-bucket-name/file.txt .

Delete File

aws s3 rm s3://my-bucket-name/file.txt

3. Sync Operations (VERY IMPORTANT)

Sync local → S3

aws s3 sync . s3://my-bucket-name/

Sync S3 → local

aws s3 sync s3://my-bucket-name/ .

Sync with delete (mirror)

aws s3 sync . s3://my-bucket-name/ --delete

4. Listing & Checking

List files in bucket
aws s3 ls s3://my-bucket-name/
List with size & date
aws s3 ls s3://my-bucket-name/ --recursive --human-readable --summarize
5. Copy & Move
Copy file within S3
aws s3 cp s3://bucket1/file.txt s3://bucket2/file.txt
Move file
aws s3 mv s3://my-bucket-name/file.txt s3://my-bucket-name/archive/file.txt
6. Access & Permissions
Make object public
aws s3 cp file.txt s3://my-bucket-name/ --acl public-read
Presigned URL (temporary access)
aws s3 presign s3://my-bucket-name/file.txt
7. Advanced (Architect-Level Commands)
Enable Versioning
aws s3api put-bucket-versioning \
--bucket my-bucket-name \
--versioning-configuration Status=Enabled
Check Versioning
aws s3api get-bucket-versioning --bucket my-bucket-name
Enable Encryption (SSE-S3)
aws s3api put-bucket-encryption \
--bucket my-bucket-name \
--server-side-encryption-configuration '{
  "Rules": [{
    "ApplyServerSideEncryptionByDefault": {
      "SSEAlgorithm": "AES256"
    }
  }]
}'
Block Public Access
aws s3api put-public-access-block \
--bucket my-bucket-name \
--public-access-block-configuration \
BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true
Lifecycle Policy (Example)
aws s3api put-bucket-lifecycle-configuration \
--bucket my-bucket-name \
--lifecycle-configuration '{
  "Rules": [{
    "ID": "MoveToGlacier",
    "Status": "Enabled",
    "Prefix": "",
    "Transitions": [{
      "Days": 30,
      "StorageClass": "GLACIER"
    }]
  }]
}'
8. Logging & Monitoring
Enable Logging
aws s3api put-bucket-logging \
--bucket my-bucket-name \
--bucket-logging-status '{
  "LoggingEnabled": {
    "TargetBucket": "log-bucket",
    "TargetPrefix": "logs/"
  }
}'
9. Static Website Hosting
Enable Website Hosting
aws s3 website s3://my-bucket-name/ \
--index-document index.html \
--error-document error.html
10. Useful Debug Command
aws s3 cp file.txt s3://my-bucket-name/ --debug
