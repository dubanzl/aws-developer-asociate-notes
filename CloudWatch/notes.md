2️⃣ What is a CloudWatch metric

In Amazon CloudWatch, a metric is simply a number measured over time.

| Metric    | Example |
| --------- | ------- |
| CPU usage | 80%     |
| Requests  | 200     |
| Errors    | 5       |


What is a custom metric

AWS services automatically send some metrics like:

Lambda invocations

EC2 CPU

DynamoDB throttling

But your payment API errors are not AWS metrics.

So you must create your own metric.

push metrics

Your Lambda function sends a metric value to CloudWatch.

Example:

If the payment API fails:

Metric name: PaymentAPIFailure
Value: 1

If it succeeds:

Metric name: PaymentAPIFailure
Value: 0

This is called publishing a custom metric.


Lambda
   ↓
Call payment API
   ↓
If failure → push metric to CloudWatch
   ↓
CloudWatch metric counts failures
   ↓
CloudWatch Alarm 
   ↓
SNS notification


2️⃣ What “high-resolution metric” means

CloudWatch normally stores metrics every 60 seconds.

High-resolution metrics store them every 1 second.

Type	Resolution
Standard	1 minute
High resolution	1 second

For monitoring error spikes quickly, AWS prefers high resolution.




| Step | Service                            | What it does                                                        | Example                           |
| ---- | ---------------------------------- | ------------------------------------------------------------------- | --------------------------------- |
| 1    | AWS Lambda                         | Calls the external payment API and detects success or failure       | Lambda processes order            |
| 2    | Amazon CloudWatch (Custom Metric)  | Lambda **pushes metrics** like `TotalRequests` and `FailedRequests` | `FailedRequests = 1`              |
| 3    | CloudWatch (Metric Storage)        | Stores metric values over time                                      | failures recorded every execution |
| 4    | CloudWatch Alarm                   | Checks if a condition is exceeded                                   | error rate > 5%                   |
| 5    | Amazon Simple Notification Service | Sends notification to support team                                  | email / Slack / SMS alert         |



Lambda
   ↓
Call Payment API
   ↓
Push Custom Metric
   ↓
CloudWatch
   ↓
Alarm (>5% failures)
   ↓
SNS Alert