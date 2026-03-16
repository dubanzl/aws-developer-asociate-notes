when you create a user in AWS you do not assign regions by default.

How IAM permissions really work

1️⃣ You create a user in IAM.

2️⃣ You attach a policy that allows actions on services like:

Amazon EC2

Amazon S3

Amazon RDS


{
  "Effect": "Allow",
  "Action": [
    "ec2:*",
    "s3:*",
    "rds:*"
  ],
  "Resource": "*"
}

IAM does not automatically restrict regions.
If the policy does not specify a region → the user can access the service in any AWS region.

{
  "Effect": "Allow",
  "Action": "ec2:*",
  "Resource": "*",
  "Condition": {
    "StringEquals": {
      "aws:RequestedRegion": "us-east-1"
    }
  }
}


aws ec2 stop-instances \
  --instance-ids i-0ab123456789abcd1 \
  --region ap-southeast-2


You define a Mappings section in CloudFormation.
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-0abcdef12345
    us-west-2:
      AMI: ami-0987654321abc
    eu-west-1:
      AMI: ami-0a1b2c3d4e5f

!FindInMap [ MapName, TopLevelKey, SecondLevelKey ]

Now you retrieve the correct AMI based on the region.

Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !FindInMap 
        - RegionMap
        - !Ref AWS::Region
        - AMI
      InstanceType: t2.micro


| Type                        | Attached to                         |
| --------------------------- | ----------------------------------- |
| **Identity-based policies** | Users, Groups, Roles                |
| **Resource-based policies** | Resources (S3 bucket, Lambda, etc.) |




2️⃣ The exception in IAM

The only resource-based policy in IAM is:

✅ Trust policy

This is the policy attached to an IAM Role.

It defines:

Who can assume the role

Example:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}

This policy is attached to the role, so it is resource-based.



--------

IAM Access Analyzer

IAM Access Analyzer simplifies inspecting unused access to guide you toward least privilege. Security teams can use IAM Access Analyzer to gain visibility into unused access across their AWS organization and automate how they rightsize permissions.