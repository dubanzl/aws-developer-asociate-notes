Main Reason to Install Kinesis Agent

👉 The purpose is to automatically stream data (like logs or metrics) from a server to AWS Kinesis without writing your own code.

Instead of building a program to send data to Kinesis, the agent does it for you

-----

Kinesis has limits per shard:

Write: 1 MB/sec or 1000 records/sec

Read: 2 MB/sec