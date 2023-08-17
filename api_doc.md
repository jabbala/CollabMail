# CollabMail API Documentation
Welcome to the API documentation for CollabMail, the collaborative mail group solution for seamless team communication.

## Base URL
The base URL for all API requests is: http://localhost:3000

## Authentication
Authentication is required for certain endpoints. Include the authentication token in the request headers.

### Example:
``` http
Authorization: Bearer YOUR_AUTH_TOKEN
```

## User Endpoints
### Register User
* URL: /api/users/register
* Method: POST
* Request Body:
``` json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "secretpassword"
}
```
* Response
``` json
{
  "success": true,
  "message": "User registered successfully"
}
```

### Login User
* URL: /api/users/login
* Method: POST
* Request Body:
``` json
{
  "email": "john@example.com",
  "password": "secretpassword"
}
```
* Response
``` json
{
  "success": true,
  "token": "YOUR_AUTH_TOKEN"
}
```
## Mail Group Endpoints
### Create Mail Group
* URL: /api/mailgroups
* Method: POST
* Request Body:
``` json
{
  "groupName": "Project Team A",
  "description": "Mail group for Project Team A"
}
```
* Response
``` json
{
  "success": true,
  "message": "Mail group created successfully",
  "groupID": 123
}
```

### Get Mail Group Details
* URL: /api/mailgroups/:groupID
* Method: GET
* Response:
```json
{
  "success": true,
  "groupID": 123,
  "groupName": "Project Team A",
  "description": "Mail group for Project Team A",
  "createdBy": "john_doe",
  "creationDate": "2023-08-17T12:34:56Z",
  "members": ["user1", "user2"],
  "emails": [
    {
      "emailID": 1,
      "sender": "user1",
      "subject": "Meeting Agenda",
      "body": "Let's discuss the upcoming meeting agenda...",
      "timestamp": "2023-08-18T10:00:00Z",
      "category": "Business"
    }
  ]
}
```

### Join Mail Group
* URL: /api/mailgroups/:groupID/join
* Method: POST
* Response:
``` json
{
  "success": true,
  "message": "Joined mail group successfully"
}
```

### Leave Mail Group
* URL: /api/mailgroups/:groupID/leave
* Method: POST
* Response:
``` json
{
  "success": true,
  "message": "Left mail group successfully"
}
```

## Email Endpoints
### Send Email
* URL: /api/emails
* Method: POST
* Request Body:
``` json
{
  "groupID": 123,
  "subject": "Meeting Reminder",
  "body": "Don't forget the meeting at 2 PM...",
  "category": "Business"
}
```
* Response:
``` json
{
  "success": true,
  "message": "Email sent successfully"
}
```
### Get Emails in Mail Group
* URL: /api/emails/:groupID
* Method: GET
* Response:
``` json
{
  "success": true,
  "emails": [
    {
      "emailID": 1,
      "sender": "user1",
      "subject": "Meeting Agenda",
      "body": "Let's discuss the upcoming meeting agenda...",
      "timestamp": "2023-08-18T10:00:00Z",
      "category": "Business"
    },
    {
      "emailID": 2,
      "sender": "user2",
      "subject": "Technical Update",
      "body": "We've made progress on the backend integration...",
      "timestamp": "2023-08-19T14:30:00Z",
      "category": "Technical"
    }
  ]
}
```

## Workflow Endpoints
### Create Workflow Instance
* URL: /api/workflows
* Method: POST
* Request Body:
``` json
{
  "templateID": 1
}
```
* Response:
``` json
{
  "success": true,
  "message": "Workflow instance created successfully",
  "instanceID": 123
} 
```
### Get Workflow Instance Details
* URL: /api/workflows/:instanceID
* Method: GET
* Response:

``` json
{
  "success": true,
  "instanceID": 123,
  "templateID": 1,
  "initiator": "john_doe",
  "startTimestamp": "2023-08-20T09:00:00Z",
  "status": "Pending",
  "currentStage": {
    "stageID": 2,
    "stageName": "Review",
    "role": "Manager",
    "actions": ["Approve", "Reject"]
  },
  "actions": [
    {
      "actionID": 1,
      "userID": "manager1",
      "stage": "Review",
      "timestamp": "2023-08-20T09:30:00Z",
      "status": "Pending"
    }
  ]
}
```

### Perform Workflow Action
* URL: /api/workflows/:instanceID/actions
* Method: POST
* Request Body:
``` json
{
  "action": "Approve",
  "comment": "Looks good"
}
```

* Response:
``` json
{
  "success": true,
  "message": "Action performed successfully"
}
```

## Access Management Endpoints
### Request Access
- URL: /api/access/request
- Method: POST
- Request Body:
``` json
{
  "groupID": 123,
  "roleID": 1
}
```
- Response:
``` json
{
  "success": true,
  "message": "Access request submitted successfully",
  "requestID": 456
}
```

### Recertification Tasks
- URL: /api/access/recertification
- Method: GET
- Response:
``` json
{
  "success": true,
  "tasks": [
    {
      "taskID": 1,
      "groupID": 123,
      "dueDate": "2023-09-30T23:59:59Z",
      "status": "Pending"
    }
  ]
}
```

### Complete Recertification
- URL: /api/access/recertification/:taskID
- Method: POST
- Response:
``` json
{
  "success": true,
  "message": "Recertification completed successfully"
}
```
### Request Revocation
- URL: /api/access/revocation
- Method: POST
- Request Body:
``` json
{
  "groupID": 123
}
```
- Response:
``` json
{
  "success": true,
  "message": "Revocation request submitted successfully",
  "requestID": 789
}
```

## Report Endpoints
### Retrieve Data for Reporting
- URL: /api/reports/data
- Method: GET
- Response:
``` json
{
  "success": true,
  "data": [
    {
      "date": "2023-08-01",
      "emailsSent": 120,
      "emailsReceived": 85,
      "workflowsInitiated": 15,
      "workflowsCompleted": 10
    },
    {
      "date": "2023-08-02",
      "emailsSent": 110,
      "emailsReceived": 90,
      "workflowsInitiated": 20,
      "workflowsCompleted": 18
    },
    // ...
  ]
}
```
### Generate Custom Reports
- URL: /api/reports/generate
- Method: POST
- Request Body:
``` json
{
  "reportType": "workflow",
  "startDate": "2023-07-01",
  "endDate": "2023-07-31",
  "groupBy": "user"
}
```
- Response:
``` json
{
  "success": true,
  "report": {
    "reportType": "workflow",
    "startDate": "2023-07-01",
    "endDate": "2023-07-31",
    "groupBy": "user",
    "data": [
      {
        "user": "john_doe",
        "workflowsInitiated": 30,
        "workflowsCompleted": 25
      },
      {
        "user": "jane_smith",
        "workflowsInitiated": 40,
        "workflowsCompleted": 35
      },
      // ...
    ]
  }
}
```

## Notification Endpoints
### Get User Notifications
* URL: /api/notifications
* Method: GET
* Response:

``` json
{
  "success": true,
  "notifications": [
    {
      "notificationID": 1,
      "type": "NewEmail",
      "timestamp": "2023-08-22T15:00:00Z",
      "data": {
        "emailID": 123,
        "sender": "user1",
        "subject": "New Task Assignment",
        "body": "You have been assigned a new task."
      }
    },
    {
      "notificationID": 2,
      "type": "ApprovalRequired",
      "timestamp": "2023-08-22T16:00:00Z",
      "data": {
        "instanceID": 456,
        "stageName": "Review",
        "initiator": "user2",
        "comment": "Please review the document."
      }
    }
  ]
}
```
