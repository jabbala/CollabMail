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
