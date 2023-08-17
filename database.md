# CollabMail
A simplified database design for the "CollabMail" project, focusing on the core entities and their relationships. Please note that this is a basic example, and you may need to expand or modify it based on your specific requirements and chosen database system.

## Entities
### User:

1. UserID (Primary Key)
2. Username
3. Email
4. Password (Hashed and Salted)
5. Registration Date

### Role:

1. RoleID (Primary Key)
2. RoleName
3. Description

### Entitlement:

1. EntitlementID (Primary Key)
2. EntitlementName
3. Description

### MailGroup:

1. GroupID (Primary Key)
2. GroupName
3. Description
4. CreatedBy (Foreign Key referencing User.UserID)
5. Creation Date

### Membership:

1. MembershipID (Primary Key)
2. GroupID (Foreign Key referencing MailGroup.GroupID)
3. UserID (Foreign Key referencing User.UserID)
4. Join Date

### Email:

1. EmailID (Primary Key)
2. GroupID (Foreign Key referencing MailGroup.GroupID)
3. SenderUserID (Foreign Key referencing User.UserID)
4. Subject
5. Body
6. Timestamp
7. Category (Business/Technical)

## Relationships:

* Each User can create multiple MailGroups.
* Each User can be a member of multiple MailGroups.
* Each MailGroup is created by one User (CreatedBy).
* Each Email belongs to one MailGroup and is sent by one User.
* Each Membership associates one User with one MailGroup.

### Role-Entitlement Relationship:

* Each Role can have multiple Entitlements.
* Each User can be assigned one or more Roles.

### User-Role Relationship:

* Each User can have one or more Roles.
