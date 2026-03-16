| Service            | Full Name                   | Main Purpose                       | Can Send Email | Can Send SMS | Typical Use Case                                  |
| ------------------ | --------------------------- | ---------------------------------- | -------------- | ------------ | ------------------------------------------------- |
| Amazon SES         | Simple Email Service        | Email delivery service             | ✅ Yes          | ❌ No         | Password reset emails, invoices, newsletters      |
| Amazon SNS         | Simple Notification Service | Publish / subscribe notifications  | ✅ Yes          | ✅ Yes        | System alerts, SMS notifications, event messaging |
| Amazon SQS         | Simple Queue Service        | Message queue between services     | ❌ No           | ❌ No         | Decouple microservices, async processing          |
| Amazon EventBridge | Event Bus                   | Event routing between AWS services | ❌ No           | ❌ No         | Event-driven architectures                        |


| Service     | Architecture Model    | Example Flow                               |
| ----------- | --------------------- | ------------------------------------------ |
| SES         | Email sending service | App → SES → User Email                     |
| SNS         | Pub/Sub messaging     | App → SNS Topic → Multiple subscribers     |
| SQS         | Queue messaging       | App → Queue → Worker processes message     |
| EventBridge | Event bus             | AWS service → EventBridge → Target service |
