# AWS Command Line Interface

The AWS Command Line Interface (CLI) is a unified tool that allows you to manage and interact with AWS services from your command line shell. It consolidates the functionality of multiple service-specific APIs and SDKs into a single, easy-to-use interface. The AWS CLI is available for Windows, macOS, and Linux operating systems.

## Features
Here are some key features of the AWS CLI:

1. **Command Autocompletion**: command autocompletion makes it easier to use by suggesting command names and options as you type. After enabling it, you can start typing a command and press the Tab key to see suggestions for command names and options. For example, type aws s3 and press Tab to see suggestions like aws s3 cp, aws s3 mv, etc.
  To enable autocompletion, follow the instructions in the official AWS CLI documentation https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-completion.html.

2. **Consistent Interface**: offers a consistent syntax and naming convention across all AWS services, which simplifies learning and reduces the complexity of managing multiple services. For example the syntax for interacting with Amazon S3 and EC2 services looks like this:
    ```
    aws s3 <s3-command> <s3-parameters>
    aws ec2 <ec2-command> <ec2-parameters>
    ```

3. **Output Formatting**: you can choose from multiple output formats (JSON, text, and table) to display the command results, making it easier to read or parse the data. You can set the default output format during configuration, or specify it with the --output option. Here's an example that lists S3 buckets in a table format:
    ```
    aws s3 ls --output table
    ```


4. **Querying and Filtering**: allows you to query and filter the command output using the `--query` option with a JMESPath expression, enabling you to extract specific data from the results. To list the instance IDs of all running EC2 instances, you can use the following command:
    ```
    aws ec2 describe-instances --query 'Reservations[*].Instances[?State.Name==`running`].InstanceId' --output text
    ```

5. **Bash Scripting**: you can use the AWS CLI in your shell scripts to automate tasks, such as creating and managing resources, deploying applications, or triggering AWS Lambda functions. To create a script to start an EC2 instance and wait for it to become available:
    ```
    #!/bin/bash
    INSTANCE_ID="i-1234567890abcdef0"
    aws ec2 start-instances --instance-ids $INSTANCE_ID
    aws ec2 wait instance-running --instance-ids $INSTANCE_ID
    echo "Instance $INSTANCE_ID is now running."
    ```

6. **AWS SDK Compatibility**: it is built on top of the AWS SDKs, which means that you can use it alongside AWS SDKs in your applications to leverage the CLI's functionality.

7. **AWS CLI Profiles**: you can create and manage multiple named profiles with different AWS credentials and configurations. This allows you to switch between different AWS accounts or regions easily. To create a new profile called "test-profile", run:
    ```
    aws configure --profile test-profile
    ```
    To use a specific profile in a command, use the ```--profile``` option:
    ```
    aws s3 ls --profile test-profile
    ```

8. **High-Level and Low-Level Commands**: provides both high-level commands that simplify complex tasks (like `aws s3 sync` for syncing directories) and low-level commands that provide granular control over service actions (like `aws s3api put-object` for uploading a single object to S3). To copy a local folder to an S3 bucket, you can use the high-level ```aws s3 sync``` command:
      ```
      aws s3 sync my-local-folder s3://my-bucket/my-folder
      ```
      To upload a single file to S3, you can use the low-level ```aws s3api put-object command```:
      aws s3api put-object --bucket my-bucket --key my-folder/my-file.txt --body my-file.txt


## Installation

To get started with the AWS CLI, you need to install it on your local machine, configure your AWS credentials, and optionally set up your default region and output format. You can then use the `aws` command followed by the service name, action, and any required or optional parameters.


Refer to the latest AWS documentation: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

After you've installed the AWS CLI, you can run `aws --version` to check the installed version. To start using the AWS CLI, you'll need to configure it with your AWS credentials using the `aws configure` command.


## Commands
This is a list of essential AWS CLI commands that you should familiarize yourself with:

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
## Tips and tricks
1. **Bash aliases for common commands**

   If you find yourself typing certain commands frequently, you can create aliases in your shell's configuration file (e.g., `~/.bashrc` for Bash or `~/.zshrc` for Zsh). For example, to create an alias for listing S3 buckets, add the following line to your shell's configuration file:
   ```
   alias s3ls="aws s3 ls"
   ```
   After reloading your shell's configuration, you can type `s3ls` instead of `aws s3 ls`.

2. **Using AWS CLI with AWS SSO**

    If you're using AWS Single Sign-On (SSO), you can configure the AWS CLI to work with SSO by running the following command:
      ```
      aws configure sso
      ```
      This command will guide you through the process of setting up the AWS CLI to work with your SSO account.

3. **Using AWS CLI in a for loop**

    You can use the AWS CLI in combination with a for loop to perform batch operations. For example, to stop all running EC2 instances in a specific region, you can use the following command:
    ```
    for instance in $(aws ec2 describe-instances --filters Name=instance-state-name,Values=running --query 'Reservations[*].Instances[*].InstanceId' --output text); do aws ec2 stop-instances --instance-ids $instance; done
    ```
4. **AWS CLI history**

AWS CLI can save a history of your commands, making it easier to review and reuse them. To enable CLI history, add the following lines to your AWS CLI configuration file `~/.aws/config`:
    ```
    [default]
    cli_history = enabled
    ```
    You can view your command history using the aws history show command. For example, to show the history of the last command, run:
    ```
    aws history show --index -1
    ```
5. **Dry run mode**

AWS CLI provides a "dry run" mode for some services, which allows you to test a command without actually executing it. This can help you avoid making unintentional changes to your resources. To perform a dry run, include the `--dry-run` option in your command. For example:
    ```
    aws ec2 stop-instances --instance-ids i-1234567890abcdef0 --dry-run
    ```
    Note that not all AWS services support the --dry-run option.

6. **Using AWS CLI with AWS Organizations**

If you're using AWS Organizations to manage multiple accounts, you can use the AWS CLI to switch between accounts by assuming an IAM role in the target account. First, configure a new CLI profile for the target account:

    aws configure set profile.target-account.role_arn arn:aws:iam::<TARGET_ACCOUNT_ID>:role/<ROLE_NAME>
    aws configure set profile.target-account.source_profile default
    
  Replace `<TARGET_ACCOUNT_ID>` and `<ROLE_NAME> with the appropriate values. Then, use the `--profile` option to run commands in the target account:

    aws s3 ls --profile target-account

To dive deeper into the AWS CLI, refer to the official AWS CLI documentation: [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)
