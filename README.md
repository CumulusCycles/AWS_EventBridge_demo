# AWS_EventBridge_demo
Code for the AWS EventBridge S3/Lambda demo [video](https://www.youtube.com/watch?v=fOYFCXv9bKI).

Invoke a Lambda Function using an S3 Event Pattern, and a Scheduled Event, in Amazon EventBridge.


## AWS CLI Commmands
```
aws s3api create-bucket --bucket YOUR_BUCKET_NAME --region YOUR_REGION

aws s3api put-bucket-notification-configuration --bucket YOUR_BUCKET_NAME --notification-configuration '{ "EventBridgeConfiguration": {} }'
```


## Lambda Function (Python)
```
import logging

LOGGER = logging.getLogger()
LOGGER.setLevel(logging.INFO)

def lambda_handler(event, context):
    LOGGER.info("Event Object from Event Rule")
    LOGGER.info(event)

    headers = {
        "Content-Type": "application/json"
    }
    body = event    
    
    return {
        'statusCode': 200,
        'headers': headers,
        'body': body
    }
```

## S3 Event Source Rule
```
{
  "detail-type": [ "Object Created", "Object Deleted"],
  "source": [
    "aws.s3"
  ],
  "detail": {
    "bucket": {
      "name": [
        "YOUR_BUCKET_NAME"
      ]
    }
  }
}
```