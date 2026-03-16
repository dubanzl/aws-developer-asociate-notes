X-Ray works across accounts

 👉 trace application requests across services

Example system:

API Gateway
   ↓
Lambda
   ↓
DynamoDB
   ↓
Another Lambda
   ↓
SQS



Here is an example of X-Ray Read-Only permissions via an IAM policy:

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "xray:GetSamplingRules",
                "xray:GetSamplingTargets",
                "xray:GetSamplingStatisticSummaries",
                "xray:BatchGetTraces",
                "xray:GetServiceGraph",
                "xray:GetTraceGraph",
                "xray:GetTraceSummaries",
                "xray:GetGroups",
                "xray:GetGroup"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}

nother example of write permissions for using X-Ray via an IAM policy:

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "xray:PutTraceSegments",
                "xray:PutTelemetryRecords",
                "xray:GetSamplingRules",
                "xray:GetSamplingTargets",
                "xray:GetSamplingStatisticSummaries"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}


For Lambda to send traces, the execution role needs this policy:

AWSXrayWriteOnlyAccess

or permissions like:

xray:PutTraceSegments
xray:PutTelemetryRecords

If the role does not have those permissions:

👉 Lambda cannot write traces
👉 X-Ray shows no data



3️⃣ How they work together

Typical Lambda tracing flow:

Request → Lambda invoked
       → X-Ray decides (sampling) if request will be traced
       → If yes:
            X-Ray SDK records internal operations
            Segments are sent to X-Ray


