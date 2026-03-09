# Developing REST APIs with Amazon API Gateway

Explanation and Hands-on Labs

------------------------------------------------------------------------

## 1. Introduction to Amazon API Gateway

Amazon API Gateway is a fully managed service that allows developers to
create, publish, secure, and monitor REST and HTTP APIs at any scale. It
acts as a front door for applications to access backend services such as
AWS Lambda, EC2, or DynamoDB.

------------------------------------------------------------------------

## 2. Key Concepts

### REST API

A type of API that uses HTTP methods like GET, POST, PUT, and DELETE.

### Resource

A logical entity accessed via a URL path (for example: /students).

### Method

An HTTP operation associated with a resource.

### Integration

Backend service connected to the API (Lambda, HTTP, Mock).

### Stage

A deployment environment such as dev, test, or prod.

### API Key

Used to control access and usage of APIs.

### Throttling

Limits the number of requests to prevent abuse.

------------------------------------------------------------------------

# LAB 1: Create a REST API (Basic)

## Objective

Create a simple REST API using Amazon API Gateway.

## Steps

1.  Login to AWS Console.
2.  Navigate to API Gateway.
3.  Click Create API.
4.  Select REST API and choose Build.
5.  API name: StudentAPI.
6.  Endpoint type: Regional.
7.  Click Create API.

------------------------------------------------------------------------

# LAB 2: Create Resources and Methods

## Objective

Add resources and HTTP methods.

## Steps

1.  Select StudentAPI.
2.  Create Resource:
    -   Resource name: students
    -   Resource path: /students
3.  Create Method:
    -   Method: GET
    -   Integration type: Mock Integration
4.  Save method.
5.  Test the GET method.

## Sample Response

{ "message": "Students API is working" }

------------------------------------------------------------------------

# LAB 3: Integrate API Gateway with AWS Lambda

## Objective

Connect REST API with backend logic.

## Steps

1.  Navigate to AWS Lambda.
2.  Create a function:
    -   Function name: GetStudentsFunction
    -   Runtime: Python 3.x
3.  Use sample code:

``` python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": "Hello from API Gateway and Lambda"
    }
```

4.  Go back to API Gateway.
5.  Edit GET method.(intergration request)
7.  Integration type: Lambda Function.
8.  Select GetStudentsFunction.
9.  Save changes.

------------------------------------------------------------------------

# LAB 4: Deploy the API

## Objective

Make the API publicly accessible.

## Steps

1.  In API Gateway, click Deploy API.
2.  Create new stage:
    -   Stage name: dev
3.  Deploy.
4.  Copy the Invoke URL.
5.  Access API: GET
    https://`<api-id>`{=html}.execute-api.`<region>`{=html}.amazonaws.com/dev/students

------------------------------------------------------------------------

# LAB 5: Secure the API (Optional)

## Objective

Restrict and monitor API access.

## Steps

1.  Enable API Key.
2.  Create Usage Plan.
3.  Attach API stage.
4.  Generate API Key.
5.  Test API using key.

------------------------------------------------------------------------

# Monitoring and Logging

Use Amazon CloudWatch to: - Monitor API latency - Track request count -
Analyze errors

------------------------------------------------------------------------

# Suggested Architecture

Client → API Gateway → Lambda → DynamoDB

------------------------------------------------------------------------

# Learning Outcomes

-   Understand REST API concepts
-   Build APIs using API Gateway
-   Integrate Lambda backend
-   Deploy and secure APIs
-   Monitor API performance

------------------------------------------------------------------------

End of Document
