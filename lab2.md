# 🔹 Lambda Function Documentation

## Overview

AWS Lambda is a serverless compute service that allows execution of code without provisioning or managing servers. In this experiment, two Lambda functions were created and orchestrated using AWS Step Functions.

---

# 📌 Lambda Function 1: HelloFunction

## Purpose

The `HelloFunction` is designed to receive input from the state machine and return a greeting message along with the received input.

---

## Procedure to Create HelloFunction

### Step 1: Navigate to AWS Lambda

1. Login to AWS Management Console  
2. Search for **Lambda**  
3. Click **Create function**

---

### Step 2: Configure Function

- Select: **Author from scratch**
- Function name: `HelloFunction`
- Runtime: Python 3.12
- Architecture: Default
- Click **Create function**

---

### Step 3: Add Function Code

Replace the default code with:

```python
def lambda_handler(event, context):
    return {
        "message": "Hello from Lambda",
        "input": event
    }
```

### Step 4: Test the Function
1. Click Test
2. Create a new test event
3. Provide sample input:
```
{
  "name": "AWS Lab"
}
```
4. click test

 # 📌 Lambda Function 2: ProcessFunction
### Purpose

The ProcessFunction receives the output from HelloFunction and processes it by wrapping it inside a new JSON structure.

### Procedure to Create ProcessFunction
#### Step 1: Create New Lambda Function
- Go to AWS Lambda
- Click Create function
- Select Author from scratch

#### Step 2: Configure Function

- Function name: ProcessFunction

- Runtime: Python 3.12

- Click Create function

#### Step 3: Add Function Code

Replace the default code with:
```
def lambda_handler(event, context):
    return {
        "status": "Processed successfully",
        "previous": event
    }
```
- Click Deploy.
- test

# part -B

## Overview

AWS Step Functions is a serverless orchestration service that coordinates multiple AWS Lambda functions into a defined workflow. In this experiment, a state machine was created to execute two Lambda functions sequentially: `HelloFunction` and `ProcessFunction`.

---

# 📌 Objective

To create a state machine that:

1. Invokes `HelloFunction`
2. Passes its output to `ProcessFunction`
3. Produces a final structured output

---

# 🛠️ Procedure to Create Step Functions State Machine

## Step 1: Navigate to AWS Step Functions

1. Login to AWS Management Console  
2. Search for **Step Functions**  
3. Click **Create state machine**

---

## Step 2: Choose Workflow Type

1. Select **Visual workflow**
2. Choose **Standard** workflow type
3. Click **Next**

Standard workflow is suitable for long-running, production-level workflows.

---

## Step 3: Add First Lambda Invoke State

1. From the left panel, drag **Lambda Invoke**
2. Drop it into the workflow canvas
3. Click the state
4. In the right configuration panel:
   - Select function: `HelloFunction`

This state will execute the first Lambda function.

---

## Step 4: Add Second Lambda Invoke State

1. Drag another **Lambda Invoke** state
2. Place it after the first state
3. Connect the first state to the second state by dragging the arrow

4. Click the second state
5. In the right configuration panel:
   - Select function: `ProcessFunction`

This state will process the output of the first function.

---

## Step 5: Verify Workflow Structure

The final workflow should look like:

Start → HelloFunction → ProcessFunction → End

This ensures sequential execution.

---

## Step 6: Configure State Machine Settings

1. Click **Next**
2. Enter:
   - State machine name: `ServerlessWorkflow`
3. Under Permissions:
   - Select **Create new role**

AWS automatically creates an IAM role that allows Step Functions to invoke Lambda functions.

4. Click **Create state machine**

---

# ▶️ Executing the State Machine

## Step 1: Start Execution

1. Open the created state machine
2. Click **Start execution**

## Step 2: Monitor Execution

- Observe the workflow graph

- Each state turns green upon successful execution

- Click the final state (ProcessFunction)

- View the Output section

### expected output

```bash 
{
  "status": "Processed successfully",
  "previous": {
    "message": "Hello from Lambda",
    "input": {
      "name": "AWS Lab"
    }
  }
} 
```
### Result

The AWS Step Functions state machine was successfully created and executed. The workflow demonstrated sequential orchestration of two AWS Lambda functions, confirming correct state transitions and output chaining.
