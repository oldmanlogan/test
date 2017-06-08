Using Lambda to Start and Stop instances
========================================

## Start Funcation 


```python

import boto3
def lambda_handler(event, context):
    region = event.get('region')
    instances = event.get('instances')
    ec2 = boto3.client('ec2', region_name=region)
    ec2.start_instances(InstanceIds=instances)
    print 'Started your instances: ' + str(instances)
```

## Stop Funcation

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
