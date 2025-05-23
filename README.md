Setup Guide


This guide walks you through deploying the Task Management System on AWS.

  -Step 1: Setup Cognito User Pool
Create a Cognito User Pool for authentication

Configure app clients and set up user sign-up/sign-in flow

Enable email verification and auto-confirmation (optional)

  -Step 2: Deploy DynamoDB Table
Create a DynamoDB table Tasks to store task metadata

Define primary key as taskId

  -Step 3: Configure Amazon RDS
Launch an RDS instance for relational data (e.g., user profiles)

Setup security groups and networking to allow Lambda access

  -Step 4: Create Lambda Functions
Create Lambda functions for:

User profile management and writing to RDS

CRUD operations for tasks (CreateTaskFunction, UpdateTaskAndNotify, DeleteTaskFunction)

File upload and management (UploadFileToTask, DeleteFileFunction)

Sending asynchronous notifications (SendNotificationEmail)

Retrieving tasks (GetTaskFunction)

Attach necessary IAM roles and permissions

Add the Lambda functions that need DB access into the VPC

  -Step 5: Set up API Gateway
Create REST API with the following endpoints:

/profile (POST)

/tasks (GET, POST)

/tasks/{taskId} (PUT, DELETE)

/tasks/{taskId}/file (DELETE)

/generate-presigned-url (POST)

/generate-download-url (GET)

Integrate API methods with Lambda functions

Enable CORS on all endpoints

  -Step 6: Configure S3 Bucket
Create an S3 bucket for storing task attachments

Setup bucket policy for secure uploads and downloads

  -Step 7: Configure SQS for Notifications
Create an SQS queue for task update notifications

Connect UpdateTaskAndNotify Lambda to publish messages

Connect SendNotificationEmail Lambda as SQS consumer

  -Step 8: Setup Monitoring and Alerts
Enable CloudWatch logging for Lambda and API Gateway

Create dashboards for performance metrics

Set alarms for errors and latency

  -Step 9: Deploy Frontend
Host the frontend static files (login.html, tasks.html, profile.html)

///////////////////////////////////////////////////////////////////////



User Manual


This manual explains how to use the Task Management System web app.


User Registration and Login
New users can sign up with their email and password

Users receive a verification email before accessing the system

Returning users log in with email and password

Task Management
After login, users see their task list with task details

Users can create new tasks with title, status, deadline, and optional file attachment

Edit existing tasks, including replacing or removing attachments

Delete tasks when no longer needed

Download attached files directly from the task list

Delete attachments independently without deleting the whole task

Profile Management
Access profile page from the top-right email link

View registered email and user info stored in RDS

Change password securely within the profile page

Log out to end the session
