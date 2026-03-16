Amazon S3 Object Lock
Purpose: Prevent files from being deleted or modified.

Feature	Purpose
Object Lock	prevent deletion
Access Advisor	show permission usage
S3 Analytics	analyze storage usage

reate an IAM role with S3 access in Account B and set Account A as a trusted entity. Create another role (instance profile) in Account A and attach it to the EC2 instances in Account A and add an inline policy to this role to assume the role from Account B


{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::awsexamplebucket1",
                "arn:aws:s3:::awsexamplebucket1/*",
                "arn:aws:s3:::awsexamplebucket2",
                "arn:aws:s3:::awsexamplebucket2/*"
            ]
        }
    ]
}

------

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::AccountB_ID:role/ROLENAME"
        }
    ]
}




What S3 Access Logging does

When you enable S3 Access Logging, AWS records every request to the bucket:

GET

PUT

DELETE

LIST

Each request creates a log file.

What happens then

1️⃣ Someone accesses the bucket
2️⃣ S3 writes a log file into the same bucket

But…

3️⃣ Writing the log file is also an S3 request

So it creates another log.

That request creates another log again.

