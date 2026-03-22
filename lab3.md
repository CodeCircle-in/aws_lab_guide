# Working with Amazon DynamoDB

Explanation and Hands-on Labs

------------------------------------------------------------------------

## 1. Introduction to Amazon DynamoDB

Amazon DynamoDB is a fully managed NoSQL database service provided by
AWS. It supports key-value and document data models and is designed for
high performance, scalability, and low latency.

### Key Features

-   Fully managed and serverless
-   Single-digit millisecond latency
-   Automatic scaling
-   On-demand billing option
-   Built-in security and backup

------------------------------------------------------------------------

## 2. Core Concepts

### Table

A collection of items.

### Item

A single record in a table (stored in JSON-like format).

### Attribute

A property of an item (similar to a column in relational databases).

### Partition Key

The primary key used to uniquely identify each item.

### Sort Key

Optional key used with partition key to enable range queries.

### Global Secondary Index (GSI)

Allows querying using non-primary key attributes.

### Local Secondary Index (LSI)

Alternate sort key with same partition key.

### RCU / WCU

Read Capacity Units and Write Capacity Units.

### TTL (Time To Live)

Automatically deletes expired items.

------------------------------------------------------------------------

# LAB 1: Creating and Using a DynamoDB Table

## Objective

Create a table and perform CRUD operations.

## Scenario

Student Management System

## Steps

1.  Login to AWS Console.
2.  Navigate to DynamoDB.
3.  Click "Create Table".
4.  Enter:
    -   Table name: Students
    -   Partition key: student_id (String)
5.  Select Billing mode: On-Demand.
6.  Click Create.

## Insert Item

Go to Explore Table → Create Item → JSON view and insert:
```
{ "student_id": "S101", "name": "Devidas", "branch": "CSE", "semester":
4, "cgpa": 8.7 }
```
## Perform Operations

-   Get Item
-   Update Item (modify CGPA)
-   Delete Item

## Learning Outcome

-   Understand DynamoDB data model
-   Perform basic CRUD operations

------------------------------------------------------------------------

# Amazon DynamoDB Lab — Part B
## Query vs Scan and Indexing

---

## Objective

To understand the performance difference between Query and Scan
operations using a Global Secondary Index (GSI).

---

## Introduction

DynamoDB provides multiple ways to retrieve data:

- Query (efficient, uses keys or indexes)
- Scan (reads the entire table)

Using indexes improves query performance.

---

## Procedure

### Step 1: Open Students Table

Navigate to: AWS Console → DynamoDB → Tables → Students


---

### Step 2: Create Global Secondary Index

Go to: Indexes → Create Index

Enter-

Index Name: branch-index
Partition Key:branch (String)
Click **Create Index**.
Wait until the index status becomes: Active



---

### Step 3: Insert Sample Data

Add multiple students.

```json
{
  "student_id": "S102",
  "name": "Harsha",
  "branch": "CSE",
  "semester": 5,
  "cgpa": 9.1
}


{
  "student_id": "S103",
  "name": "Rahul",
  "branch": "ISE",
  "semester": 4,
  "cgpa": 8.4
}


{
  "student_id": "S104",
  "name": "Anita",
  "branch": "CSE",
  "semester": 3,
  "cgpa": 8.9
}

