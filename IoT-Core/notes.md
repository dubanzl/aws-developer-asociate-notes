| Feature             | IoT Core ✅         | API Gateway ❌     |
| ------------------- | ------------------ | ------------------- |
| Protocol            | MQTT (lightweight) | HTTP (heavier)      |
| Connection          | Persistent         | Request/response    |
| Auth                | X.509 certificates | IAM / JWT / Cognito |
| Designed for        | IoT devices        | Web/mobile apps     |
| Battery efficient   | ✅ Yes              | ❌ No              |
| Millions of devices | ✅ Yes              | ⚠️ Not ideal       |


| Service        | What it does                    | When to use                  |
| -------------- | ------------------------------- | ---------------------------- |
| **IoT Core**   | Connect devices to AWS securely | Always for IoT communication |
| **Greengrass** | Run logic on devices locally    | Edge computing / offline     |
| **Private CA** | Create your own certificates    | Custom enterprise security   |
| **ACM**        | HTTPS certificates for apps     | Websites / APIs              |
