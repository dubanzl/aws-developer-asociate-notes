Throttling – Maximum sending rate exceeded”

This means you are sending emails faster than SES allows per second.


| Attempt | Delay             |
| ------- | ----------------- |
| 1       | retry immediately |
| 2       | wait 1 second     |
| 3       | wait 2 seconds    |
| 4       | wait 4 seconds    |
| 5       | wait 8 seconds    |

| Situation               | AWS Best Practice   |
| ----------------------- | ------------------- |
| Service throttling      | Exponential backoff |
| API rate exceeded       | Exponential backoff |
| Temporary service limit | Retry with backoff  |

Example

import boto3
from botocore.config import Config

config = Config(
    retries={
        'max_attempts': 5,
        'mode': 'standard'
    }
)

ses = boto3.client('ses', config=config)

response = ses.send_email(
    Source='sender@example.com',
    Destination={'ToAddresses': ['user@example.com']},
    Message={
        'Subject': {'Data': 'Hello'},
        'Body': {'Text': {'Data': 'Test email'}}
    }
)