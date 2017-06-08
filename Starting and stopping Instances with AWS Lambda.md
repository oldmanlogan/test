Using Lambda to Start and Stop instances
========================================

## Start Function 


```python

import boto3
def lambda_handler(event, context):
    region = event.get('region')
    instances = event.get('instances')
    ec2 = boto3.client('ec2', region_name=region)
    ec2.start_instances(InstanceIds=instances)
    print 'Started your instances: ' + str(instances)
```

## Stop Function

```python

import boto3
def lambda_handler(event, context):
    region = event.get('region')
    instances = event.get('instances')
    ec2 = boto3.client('ec2', region_name=region)
    ec2.stop_instances(InstanceIds=instances)
    print 'Stopping your instances: ' + str(instances)

```

## Custom Policy for Lambda Role 
This is a very basic policy please use with caution!

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "arn:aws:logs:*:*:*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:Start*",
                "ec2:Stop*"
            ],
            "Resource": "*"
        }
    ]
}

```
cloudwatch rule lambda contrant example.

```json

{
    "region": "eu-west-1",
    "instances": ["i-0c70057f8e0774115"]
}

```
