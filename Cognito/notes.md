1️⃣ Cognito User Pools

User Pools provide:

Sign up

Sign in

Passwords

JWT tokens

MFA

Mobile app
   ↓
Cognito User Pool
   ↓
User logs in

But User Pools do NOT give AWS permissions directly.


2️⃣ Cognito Identity Pools

User login (Google, Facebook, Cognito)
           ↓
      Identity Pool
           ↓
 Temporary AWS credentials
           ↓
        DynamoDB

Used for authorization to AWS resources.


| Question type                    | Service       |
| -------------------------------- | ------------- |
| Login / sign up / authentication | User Pool     |
| Access AWS services directly     | Identity Pool |
