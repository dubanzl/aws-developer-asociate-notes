multi-tenant
AWS physical server
 ├── Company A VM
 ├── Company B VM
 └── Company C VM

single-tenant
AWS physical server
 └── Only your company EC2 instances

A cybersecurity company might require:

No other customer workloads
on the same physical hardware

Even though AWS isolation is already strong, some regulations require dedicated hardware.


| Option              | Cost      | Single tenant |
| ------------------- | --------- | ------------- |
| Spot                | cheap     | ❌             |
| On-Demand           | medium    | ❌             |
| Dedicated Instances | moderate  | ✅             |
| Dedicated Hosts     | expensive | ✅             |


Network ACL: NACL can block traffic before it even reaches the instance.

Internet
   ↓
NACL (subnet firewall)
   ↓
Security Group (instance firewall)
   ↓
EC2


----
SAM focuses mainly on:

Lambda

API Gateway

DynamoDB

Step Functions

But not Cognito user pools directly.


| SAM Resource                  |
| ----------------------------- |
| AWS::Serverless::Function     |
| AWS::Serverless::Api          |
| AWS::Serverless::HttpApi      |
| AWS::Serverless::SimpleTable  |
| AWS::Serverless::Application  |
| AWS::Serverless::StateMachine |


EC2 Instance
     │
     ▼
Public Subnet
     │
     ▼
Route Table
0.0.0.0/0 → Internet Gateway
     │
     ▼
Internet Gateway
     │
     ▼
Internet


2️⃣ How Reserved Instances work

A Reserved Instance does NOT limit how many instances you can run.

Instead, it gives a billing discount.

Think of it like a coupon.

You bought 1 coupon for m4.xlarge.

AWS will automatically apply that coupon to one instance.