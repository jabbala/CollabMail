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

### WorkflowTemplate:

- TemplateID (Primary Key)
- TemplateName
- Description

### WorkflowStage:

- StageID (Primary Key)
- TemplateID (Foreign Key referencing WorkflowTemplate.TemplateID)
- StageName
- RoleID (Foreign Key referencing Role.RoleID)
- Actions (JSON Array of role-based actions)

### WorkflowInstance:

- InstanceID (Primary Key)
- TemplateID (Foreign Key referencing WorkflowTemplate.TemplateID)
- InitiatorUserID (Foreign Key referencing User.UserID)
- StartTimestamp
- Status (Pending/Approved/Rejected)
- CurrentStageID (Foreign Key referencing WorkflowStage.StageID)

### WorkflowAction:

- ActionID (Primary Key)
- InstanceID (Foreign Key referencing WorkflowInstance.InstanceID)
- UserID (Foreign Key referencing User.UserID)
- StageID (Foreign Key referencing WorkflowStage.StageID)
- ActionTimestamp
- Comment
- Status (Pending/Approved/Rejected)

### Notification:

- NotificationID (Primary Key)
- UserID (Foreign Key referencing User.UserID)
- EmailID (Foreign Key referencing Email.EmailID)
- Type (NewEmail/NewWorkflow/TaskAssigned/ApprovalRequired/etc.)
- Timestamp

## Relationships:

- Each User can create multiple MailGroups.
- Each User can be a member of multiple MailGroups.
- Each MailGroup is created by one User (CreatedBy).
- Each Email belongs to one MailGroup and is sent by one User.
- Each Membership associates one User with one MailGroup.
- Each Role can have multiple Entitlements.
- Each User can have one or more Roles.
- Each WorkflowTemplate can have multiple WorkflowStages.
- Each WorkflowInstance belongs to one WorkflowTemplate and is initiated by one User.
- Each WorkflowStage is associated with one Role.
- Each WorkflowAction is associated with one WorkflowInstance, one User, and one WorkflowStage.
- Each Notification is associated with one User and may reference an Email.
