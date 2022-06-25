### Create S3 bucket
```
aws s3api create-bucket --bucket bucket-name --region ap-southeast-1 --create-bucket-configuration LocationConstraint=ap-southeast-1
```
