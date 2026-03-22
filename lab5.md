# Experiment 5: Creating Lambda Functions Using AWS SDK for Python (Boto3)

## Aim

To create and deploy an AWS Lambda function programmatically using the
AWS SDK for Python (Boto3) through AWS CloudShell.

------------------------------------------------------------------------

## Objective

-   Understand AWS SDK for Python (Boto3)
-   Create Lambda functions using Python scripts
-   Deploy Lambda functions without using the AWS Console
-   Automate AWS resource creation

------------------------------------------------------------------------

## Introduction

AWS Lambda is a serverless compute service that allows users to run code
without provisioning or managing servers. It automatically scales and
executes code in response to events.

The AWS SDK for Python, known as **Boto3**, allows developers to
interact with AWS services programmatically. Using Boto3, developers can
automate tasks such as:

-   Creating Lambda functions
-   Uploading code
-   Managing AWS resources
-   Integrating AWS services

In this experiment, a Lambda function is created programmatically using
a Python script executed inside AWS CloudShell.

------------------------------------------------------------------------

## Services Used

-   AWS CloudShell
-   AWS Lambda
-   AWS SDK for Python (Boto3)
-   AWS IAM

------------------------------------------------------------------------

## Architecture

CloudShell\
↓\
Python Script (Boto3)\
↓\
AWS Lambda Service\
↓\
Lambda Function Created

------------------------------------------------------------------------

## Prerequisites

-   AWS Account
-   Access to AWS CloudShell
-   IAM Role for Lambda execution
-   Basic knowledge of Python

------------------------------------------------------------------------

# Creating IAM Role for Lambda Execution

AWS Lambda requires an execution role that grants permission to access
other AWS services such as CloudWatch Logs.

### Step 1: Open IAM

1.  Login to AWS Management Console
2.  Navigate to **IAM (Identity and Access Management)**

### Step 2: Create Role

1.  Click **Roles**
2.  Click **Create role**
3.  Choose:

Trusted entity type: AWS Service\
Use case: Lambda

Click **Next**.

### Step 3: Attach Permissions

Attach the policy:

AWSLambdaBasicExecutionRole

This policy allows Lambda to write logs to Amazon CloudWatch.

Click **Next**.

### Step 4: Name the Role

Role name:

lambda-role

Click **Create role**.

### Step 5: Copy Role ARN

Example:

arn:aws:iam::123456789012:role/lambda-role

This ARN will be used in the Python script.

------------------------------------------------------------------------

# Procedure

## Step 1: Open AWS CloudShell

1.  Login to AWS Console
2.  Click the **CloudShell icon**
3.  Wait for the terminal to start

------------------------------------------------------------------------

## Step 2: Create Lambda Function Code

Create a file:

nano lambda_function.py

Add the following code:
```
def lambda_handler(event, context): 
  return "Hello from Lambda created using Boto3"
```
Save the file.

------------------------------------------------------------------------

## Step 3: Create Deployment Package

Compress the Lambda code.
```
zip function.zip lambda_function.py
```
------------------------------------------------------------------------

## Step 4: Create Python Script

Create a new file:
```
nano create_lambda.py
```
Add the following code:
```
import boto3

lambda_client = boto3.client('lambda')

with open('function.zip','rb') as f: zipped_code = f.read()

response = lambda_client.create_function( FunctionName='HelloLambdaSDK',
Runtime='python3.12', Role='arn:aws:iam::123456789012:role/lambda-role',
Handler='lambda_function.lambda_handler',
Code=dict(ZipFile=zipped_code), Timeout=15, MemorySize=128, Publish=True
)

print(response)
```
Replace the account ID with your own AWS account ID.

------------------------------------------------------------------------

## Step 5: Run the Python Script

Execute the script in CloudShell.
```
python3 create_lambda.py
```
If successful, the Lambda function will be created automatically.

------------------------------------------------------------------------

## Step 6: Verify the Lambda Function

1.  Navigate to **AWS Console → Lambda**
2.  Find the function:HelloLambdaSDK

3.  Open the function and click **Test**.

you will see the results as "Hello from Lambda created using Boto3" if successful

------------------------------------------------------------------------

## Result

A Lambda function named **HelloLambdaSDK** was successfully created
using the AWS SDK for Python (Boto3). The function was deployed
programmatically through AWS CloudShell and executed successfully.

------------------------------------------------------------------------

## Conclusion

This experiment demonstrates how AWS services can be automated using the
AWS SDK for Python. Instead of manually creating resources through the
AWS Console, developers can automate cloud resource management using
Python scripts and Boto3.

------------------------------------------------------------------------

## Learning Outcomes

-   Understand AWS Lambda serverless architecture
-   Use AWS SDK for Python (Boto3)
-   Automate Lambda deployment
-   Execute and test Lambda functions
