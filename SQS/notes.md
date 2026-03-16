# aws cloudformation create-stack \
#   --stack-name sqs-test-stack \
#   --template-body file://sqs-test.yaml

# aws cloudformation wait stack-create-complete \
#   --stack-name sqs-test-stack


# aws cloudformation describe-stacks \
#   --stack-name sqs-test-stack \
#   --query "Stacks[0].Outputs[?OutputKey=='QueueUrl'].OutputValue" \
#   --output text


# QUEUE_URL="paste-the-queue-url-here"

# aws sqs send-message \
#   --queue-url "$QUEUE_URL" \
#   --message-body "Hello from CloudFormation test"


# aws sqs receive-message \
#   --queue-url "$QUEUE_URL" \
#   --wait-time-seconds 10 \
#   --max-number-of-messages 1

You will get something like this:

{
  "Messages": [
    {
      "MessageId": "1234-example",
      "ReceiptHandle": "AQEB....example....",
      "Body": "Hello from CloudFormation test"
    }
  ]
}

aws sqs delete-message \
  --queue-url "$QUEUE_URL" \
  --receipt-handle "paste-receipt-handle-here"


  aws sqs delete-queue \
  --queue-url "$QUEUE_URL"

  aws cloudformation delete-stack \
  --stack-name sqs-test-stack


Quick exam trick

Create queue → CloudFormation resource: AWS::SQS::Queue

Send one message → SendMessage

Read one message → ReceiveMessage

Delete one message → DeleteMessage

Delete entire queue and contents → DeleteQueue

Delete all messages but keep queue → PurgeQueue


What is a Dead-Letter Queue (DLQ)

A Dead-Letter Queue is a queue where failed messages go.

Producer → Main Queue → Worker
                      ↓
                 Message fails
                      ↓
                 Dead Letter Queue

  

Visibility Timeout?
When a consumer receives a message from SQS, the message is hidden temporarily so other consumers don't process it at the same time.

3️⃣ The timeout part

The message stays invisible for a period of time.

Default: 30 seconds

0 sec   → Worker receives message
0–30 sec → Message invisible to others
30 sec  → If not deleted, message appears again



MessageRetentionPeriod

Controls how long the message exists

Message enters queue
↓
Stored for X days
↓
Deleted if unused


DelaySeconds

Controls when the message becomes visible

Message sent
↓
Wait 30 seconds
↓
Consumers can read it

-----------

 There are no message limits for storing in SQS, but 'in-flight messages' do have limits. Make sure to delete messages after you have processed them


 ----
 Use delay queues to postpone the delivery of new messages to the queue for a few seconds