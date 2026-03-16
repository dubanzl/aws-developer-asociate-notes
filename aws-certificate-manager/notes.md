
IAM certificate method (old)
You had to create them yourself using tools like:

OpenSSL
Let's Encrypt
Other CA

openssl req -new -newkey rsa:2048 -nodes -keyout key.pem -out csr.pem

aws iam upload-server-certificate

Simple comprarison

| Service | Create certificate | Upload certificate |
| ------- | ------------------ | ------------------ |
| ACM     | ✅ Yes              | ❌ No             |
| IAM     | ❌ No               | ✅ Yes            |
