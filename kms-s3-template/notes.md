
Today AWS usually calls it KMS key, but CMK is the older name you will still see in documentation and exams.

Think of it like a secure vault.

Your App  → asks KMS to encrypt something
KMS       → uses the CMK internally
KMS       → returns encrypted result

Run this command:

aws cloudformation deploy \
  --template-file kms-s3-template.yaml \
  --stack-name kms-s3-encryption-demo \
  --capabilities CAPABILITY_NAMED_IAM