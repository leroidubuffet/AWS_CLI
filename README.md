# AWS Command Line Interface

The AWS Command Line Interface (CLI) is a powerful tool that allows you to interact with AWS services using commands in your command line shell. Here is a list of essential AWS CLI commands that you should familiarize yourself with:


1. **Configure**: Set up and manage the AWS CLI on your local machine.
```
aws configure
```

2. **S3**: Interact with Amazon S3, a simple storage service for storing and retrieving objects.
- List buckets:
  ```
  aws s3 ls
  ```
- Copy files to/from S3:
  ```
  aws s3 cp localfile s3://bucketname/objectkey
  aws s3 cp s3://bucketname/objectkey localfile
  ```
- Sync local directory with S3 bucket:
  ```
  aws s3 sync localdir s3://bucketname
  ```

3. **EC2**: Manage Amazon EC2 instances, which are virtual servers in the AWS cloud.
- Describe instances:
  ```
  aws ec2 describe-instances
  ```
- Start/stop instances:
  ```
  aws ec2 start-instances --instance-ids i-1234567890abcdef0
  aws ec2 stop-instances --instance-ids i-1234567890abcdef0
  ```

4. **Lambda**: Manage AWS Lambda functions, which are serverless compute services that run your code in response to events.
- Create function:
  ```
  aws lambda create-function --function-name my-function --runtime nodejs14.x --role arn:aws:iam::123456789012:role/service-role/my-service-role --handler index.handler --zip-file fileb://my-function.zip
  ```
- Update function code:
  ```
  aws lambda update-function-code --function-name my-function --zip-file fileb://my-function.zip
  ```

5. **DynamoDB**: Interact with Amazon DynamoDB, a managed NoSQL database service.
- List tables:
  ```
  aws dynamodb list-tables
  ```
- Create table:
  ```
  aws dynamodb create-table --table-name my-table --attribute-definitions AttributeName=ID,AttributeType=N --key-schema AttributeName=ID,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5
  ```

6. **IAM**: Manage AWS Identity and Access Management (IAM), which helps you securely control access to AWS resources.
- List users:
  ```
  aws iam list-users
  ```
- Create role:
  ```
  aws iam create-role --role-name my-role --assume-role-policy-document file://trust-policy.json
  ```

7. **API Gateway**: Manage Amazon API Gateway, a fully managed service for creating, publishing, and maintaining RESTful APIs.
- List APIs:
  ```
  aws apigateway get-rest-apis
  ```

8. **CloudWatch**: Monitor AWS resources and applications using Amazon CloudWatch, a monitoring and observability service.
- List metrics:
  ```
  aws cloudwatch list-metrics
  ```
- Get metric data:
  ```
  aws cloudwatch get-metric-data --metric-data-queries file://queries.json --start-time 2023-04-01T00:00:00Z --end-time 2023-04-13T00:00:00Z
  ```

To dive deeper into the AWS CLI, refer to the official AWS CLI documentation: [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)
