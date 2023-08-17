# CollabMail
A simplified database design for the "CollabMail" project, focusing on the core entities and their relationships. Please note that this is a basic example, and you may need to expand or modify it based on your specific requirements and chosen database system.

## Entities
### User:

UserID (Primary Key)
Username
Email
Password (Hashed and Salted)
Registration Date

### MailGroup:

GroupID (Primary Key)
GroupName
Description
CreatedBy (Foreign Key referencing User.UserID)
Creation Date

### Membership:

MembershipID (Primary Key)
GroupID (Foreign Key referencing MailGroup.GroupID)
UserID (Foreign Key referencing User.UserID)
Join Date

### Email:

EmailID (Primary Key)
GroupID (Foreign Key referencing MailGroup.GroupID)
SenderUserID (Foreign Key referencing User.UserID)
Subject
Body
Timestamp
Category (Business/Technical)

## Relationships:

Each User can create multiple MailGroups.
Each User can be a member of multiple MailGroups.
Each MailGroup is created by one User (CreatedBy).
Each Email belongs to one MailGroup and is sent by one User.
Each Membership associates one User with one MailGroup.

## Database Design Considerations: (Personal Note)

Use appropriate data types for each attribute (e.g., VARCHAR for strings, DATETIME for timestamps).
Set up foreign key constraints to maintain data integrity.
Implement proper indexing for efficient querying, especially for frequently accessed attributes.
