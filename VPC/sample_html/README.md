 
## [How to create AWS S3 bucket as a static website with AWS CLI](https://blog.eq8.eu/til/create-aws-s3-bucket-as-static-website-with-cli.html)


Create AWS S3 bucket as a static website with AWS CLI - Example static website for article: 
<https://blog.eq8.eu/til/create-aws-s3-bucket-as-static-website-with-cli.html>



## run



```bash
echo '{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::happy-bunny/*"
        }
    ]   
}' > /tmp/bucket_policy.json

aws s3api create-bucket --bucket happy-bunny --region eu-west-1  --create-bucket-configuration LocationConstraint=eu-west-1
aws s3api put-bucket-policy --bucket happy-bunny --policy file:///tmp/bucket_policy.json
aws s3 sync /tmp/SOURCE_FOLDER s3://happy-bunny/
aws s3 website s3://happy-bunny/ --index-document index.html --error-document error.html 
```
