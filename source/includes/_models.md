# Models

## Action

> Sample JSON

```json
{
    "actionId": "a-00000001",
    "actionType": "amazon-start-ec2-instances",
    "actionVersionId": "av-00000001",
    "comments": "Comments about this action",
    "credentialId": "cred-00000001",
    "isCurrentVersion": true,
    "isEnabled": true,
    "lastModifiedBy": "u-00000001",
    "lastModifiedDate": "2016-06-09T12:21:00Z",
    "managedInstanceId": "mi-00000001",
    "name": "Start My Instances",
    "nextExecutionDate": "2016-06-10T12:23:00Z",
    "regionName": "us-east-1",
  	"schedule": {
    	"scheduleType": "daily",
        "startDate": "2016-06-10",
        "timeOfDay": "12:23:00",
        "timeZoneId": "Eastern Standard Time",
        "parameters": {
        	"days": [
            	"monday",
                "tuesday",
                "wednesday",
                "thursday",
                "friday"
            ]
        }
    },
    "tags": [
    	"cost-reduction"
    ]
}
```

Represents an action.

Property | Type | Description
-------- | ---- | -----------
actionId | string | ID of the action.
actionType | string | Type ID of the action.
actionVersionId | string | Version ID of the action.
comments | string | User notes for the action.
credentialId | string | ID of the credential.
displayData | object | General purpose display data.
lastExection | <a href="#actionexecution">object</a> | Action execution data for the last execution of this action.
isCurrentVersion | boolean | True if the action version is the latest.
isEnabled | boolean | True if the action is enabled to execute. False otherwise.
lastModifiedBy | string | ID of the user whom last modified the action.
lastModifiedDate | string | Date, in ISO 8601 format, at which the action was last modified.
managedInstanceId | string | ID of the Managed Instance to which this action belongs.
name | string | Name of the action.
nextExecutionDate | string | Date, in ISO 8601 format, at which the action will next execute.
parameters | object | Additional action parameters specific to the action type.
regionName | string | Region system name in which the action will execute.
runningCount | integer | Number of currently running exections of this action.
schedule | object | Schedule for the action.
snsEndpoint | string | SNS endpoint to trigger the action.
tags | array of string | Tags for the action.

The `displayData`, `lastExecution`, `parameters`, and `runningCount` properties are only populated when requested as part of the request's `include` parameter.

## ActionExecution

> Sample JSON

```json
{
    "actionExecutionId": "ae-00000001",
    "actionId": "a-00000001",
    "actionName": "Start My Instances",
    "actionType": "amazon-start-ec2-instance",
    "actionVersionId": "av-00000001",
    "credentialId": "cred-00000001",
    "endDate": "2016-06-01T12:03:00Z",
    "managedInstanceId": "mi-00000001",
    "result": {
        "code": 0,
        "text": "Execution succeeded"
    },
    "startDate": "2016-06-01T12:00:00Z",
    "status": "complete",
    "timeZoneId": "UTC",
    "trigger": "schedule"
}
```

Represents a single execution of an action.

Property | Type | Description
-------- | ---- | -----------
actionExecutionId | string | ID of the action execution
actionId | string | ID of the action that was executed.
actionName | string | Name of the action.
actionType | string | Type ID of the action.
actionVersionId | string | Version ID of the action that was executed.
credentialId | string | ID of the credential.
endDate | string | Date, in ISO8601 format, when the action finished. Will not be present if the status is not "complete".
managedInstanceId | string | ID of the Managed Instance in which the action belongs. Will not be present if the action is not part of a Managed Instance.
result | <a href="#actionexecutionresult">object</a> | Will not be present if the status is not "complete".
startDate | string | Date, in ISO8601 format, when the action started.
status | string | Status of the execution. Valid values include: running, complete, cancelling.
timeZoneId | string | ID of the time zone for the action.
trigger | string | Trigger which started the action. Valid values include: schedule, user, sns.

## ActionExecutionResult

> Sample JSON

```json
{
    "code": 0,
    "text": "Execution succeeded"
}
```

Specifies the result of an action execution.

Property | Type | Description
-------- | ---- | -----------
code | integer | Result code.
text | string | Resulting text message.

## AmazonIamRoleExternalId

> Sample JSON

```json
{
	"expiryDate": "2016-06-07T20:21:00Z",
    "externalId": "skeddly-12345678"
}
```

A generated external ID for an IAM role.

Property | Type | Description
-------- | ---- | -----------
expiryDate | string | Date, in ISO8601 format, when the external ID will expire. The external ID must be used to create an IAM role before the expiry date.
externalId | string | Generated external ID to be used in the trust relationship of the IAM role.

## AttachManagedPolicy

> Sample JSON

```json
{
	"managedPolicyId": "full"
}
```

Specifies the managed policy to attach to a user.

Property | Type | Description
-------- | ---- | -----------
managedPolicyId | string | Required. ID of the managed policy to attach to the user.

## CreateCredential

> Sample JSON for registering an IAM role

```json
{
	"cloudProviderSubTypeId": "amazon-standard",
    "credentialType": "amazon-iam-role",
    "externalId": "skeddly-12345678",
    "name": "My Credentials",
    "roleArn": "arn:aws:iam:123456789012::role/Skeddly"
}
```

> Sample JSON for registering an IAM access key

```json
{
	"accessKeyId": "AK123456789012345678",
	"cloudProviderSubTypeId": "amazon-standard",
    "credentialType": "amazon-access-key",
    "name": "My Credentials",
    "secretAccessKey": "1234567890123456789012345678901234567890"
}
```

Specifies the credential information when registering credentials.

Property | Type | Description
-------- | ---- | -----------
accessKeyId | string | Conditional. Access key of the IAM user.
cloudProviderSubTypeId | string | Required. Cloud-provider sub-type ID. Valid values include: amazon-standard, amazon-govcloud-us, amazon-china.
credentialType | string | Required. Type of credential being registered. Valid values include: amazon-iam-role, amazon-access-key.
externalId | string | Conditional. External ID used with the IAM role. Must have been generated using <a href="#credentialsgenerateiamroleexternalid"></a>.
name | string | Required. Friendly name for the credential.
roleArn | string | Conditional. ARN for the IAM role being registered.
secretAccessKey | string | Conditional. Secret access key of the IAM user.

If registering an IAM role, then `roleArn` and `externalId` are required.

If registering an access key, then `accessKeyId` and `secretAccessKey` are required.

## CreateManagedInstanceGroup

> Sample JSON

```json
{
	"backupParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "23:00:00",
            "parameters": {
            	"days": [
                	"sunday",
                    "monday",
                    "tuesday",
                    "wednesday",
                    "thursday",
                    "friday",
                    "saturday"
                ]
            }
        },
        "backupName": "daily-backup-$(DATE)",
        "tags": [
        	{
            	"name": "Created by",
                "value": "Skeddly"
            }
        ]
    },
    "deleteBackupsParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "03:00:00",
            "parameters": {
            	"days": [
                	"saturday"
                ]
            }
        },
        "olderThanDays": 7,
        "minimumToKeep": 2,
        "isPerVolume": true
    },
    "name": "My Group",
    "startStopParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "08:00:00",
            "parameters": {
            	"days": [
                	"monday",
                    "tuesday",
                    "wednesday",
                    "thursday",
                    "friday"
                ]
            }
        },
        "stopTimeInSeconds": 43200
    },
    "timeZoneId": "UTC"
}
```

Specification for a new Managed Instance Group.

Property | Type | Description
-------- | ---- | -----------
backupParameters | <a href="#managedinstancebackupparameters">object</a> | Parameters for the instance backup.
deleteBackupsParameters | <a href="#managedinstancedeletebackupsparameters">object</a> | Parameters for the instance backup deletions.
name | string | Required. Name of the Managed Instance Group.
startStopParameters | <a href="#managedinstancestartstopparameters">object</a> | Parameters for starting and stopping the instance.
timeZoneId | string | Required. ID of the time zone in which the Managed Instance Group will execute.

## CreateUser

> Sample JSON

```json
{
	"emailAddress": "user@example.com",
    "managedPolicyIds": [
    	"full"
    ],
    "username": "user1",
    "password": "reallygoodpassword"
}
```

Specification for a new user.

Property | Type | Description
-------- | ---- | -----------
emailAddress | string | Required. Email address for the new user. It must not already be used by another user.
managedPolicyIds | array of string | List of Managed Policy IDs to apply to the new user.
password | string | Required. Password for the new user.
username | string | Required. Username for the new user.

<aside class="notice">
Usernames and email addresses must be unique across all users of all Skeddly accounts. 
</aside>

Many email servers support "+ notation" to support unique passwords for a single inbox. For example, if the real email address was "user@example.com", then "user+skeddly@example.com" would forward to the same inbox. Essentially, everything between the "+" and "@" characters is ignored. Check with your IT team to see if your email servers support "+ notation".

## Credential

> Sample JSON for an IAM role

```json
{
	"actionIds": [
    	"a-00000001"
    ],
	"cloudProviderSubTypeId": "amazon-standard",
	"createdDate": "2016-06-08T14:42:00Z",
	"credentialId": "cred-00000001",
    "credentialType": "amazon-iam-role",
    "externalId": "skeddly-12345678",
    "isUsedForSnsNotifications": false,
    "lastModifiedDate": "2016-06-08T14:42:00Z",
    "lastModifiedBy": "u-00000001",
    "managedInstanceIds": [
    	"mi-00000001"
    ],
    "name": "My Credential",
    "roleArn": "arn:aws:iam::123456789012:role/Skeddly",
    "status": "active"
}
```

Specification for a new user.

Property | Type | Description
-------- | ---- | -----------
accessKeyId | string | Access key of the IAM user.
actionIds | array of string | IDs of the actions using the credential.
cloudProviderSubTypeId | string | Cloud-provider sub-type ID. Valid values include: amazon-standard, amazon-govcloud-us, amazon-china.
createdDate | string | Date, in ISO 8601 format, when the credential was registered.
credentialId | string | ID of the credential.
credentialType | string | Type of credential being registered. Valid values include: amazon-iam-role, amazon-access-key.
externalId | string | External ID used with the IAM role.
isUsedForSnsNotifications | boolean | True if the credential is configured to send SNS notifications. False otherwise.
lastModifiedDate | string | Date, in ISO 8601 format, when the credential was last modified.
lastModifiedBy | string | ID of the user whom last modified the credential.
managedInstanceIds | array of string | IDs of the Managed Instances using the credential.
name | string | Friendly name for the credential.
roleArn | string | ARN for the IAM role being registered.
secretAccessKey | string | Secret access key of the IAM user.
status | string | Status of the credential. Valid values include: active, deleted.

If `credentialType` is "amazon-iam-role", then `roleArn` and `externalId` will be present.

If `credentialType` is "amazon-access-key", then `accessKeyId` and `secretAccessKey` will be present.

## DailyScheduleParameters

> Sample JSON

```json
{
	"days": [
    	"sunday",
        "monday",
        "tuesday",
        "wednesday",
        "thursday",
        "friday",
        "saturday"
    ]
}
```

Specification for parameters specific to a daily schedule.

Derived from <a href="#scheduleparameters">ScheduleParameters</a> and includes all properties.

Property | Type | Description
-------- | ---- | -----------
days | array of string | Array of days of the week. Possible values include: sunday, monday, tuesday, wednesday, thursday, friday, saturday.

## DetachManagedPolicy

> Sample JSON

```json
{
	"managedPolicyId": "full"
}
```

Specifies the managed policy to detacxh from a user.

Property | Type | Description
-------- | ---- | -----------
managedPolicyId | string | Required. ID of the managed policy to detach from the user.

## HourlyScheduleParameters

> Sample JSON

```json
{
	"hours": [
    	0,
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        10,
        11,
        12,
        13,
        14,
        15,
        16,
        17,
        18,
        19,
        20,
        21,
        22,
        23
    ]
}
```

Specification for parameters specific to a hourly schedule.

Derived from <a href="#scheduleparameters">ScheduleParameters</a> and includes all properties.

Property | Type | Description
-------- | ---- | -----------
hours | array of integers | Array of hours of the day. Possible values include integers from 0 to 23.

## ManagedInstanceBackupParameters

```json
{
	"backupName": "daily-backup-$(DATE)",
    "schedule": {
    	"scheduleType": "daily",
        "timeOfDay": "23:00:00",
        "parameters": {
            "days": [
                "sunday",
                "monday",
                "tuesday",
                "wednesday",
                "thursday",
                "friday",
                "saturday"
            ]
        }
    },
    "tags": [
    	{
        	"name": "Created by",
            "value": "Skeddly"
        }
    ]
}
```

Specification for parameters specific to a backup schedule.

Property | Type | Description
-------- | ---- | -----------
backupName | string | Name to use when creating the backup.
schedule | <a href="#managedinstanceschedule">object</a> | Schedule for the backup.
tags | array of object | Tags to add to the backup.

## ManagedInstanceDeleteBackupsParameters

```json
{
	"isPerVolume": true,
    "minimumToKeep": 2,
    "olderThanDays": 7,
    "schedule": {
    	"scheduleType": "daily",
        "timeOfDay": "23:00:00",
        "parameters": {
            "days": [
                "sunday",
                "monday",
                "tuesday",
                "wednesday",
                "thursday",
                "friday",
                "saturday"
            ]
        }
    }
}
```

Specification for parameters specific to a backup schedule.

Property | Type | Description
-------- | ---- | -----------
isPerVolume | boolean | Applies when deleting EBS snapshots only.
minimumToKeep | integer | Minimum number of backups to preserve.
olderThanDays | integer | Minimum age for a backup to be deleted.
schedule | <a href="#managedinstanceschedule">object</a> | Schedule for the deletion of backups.

## ManagedInstanceGroup

> Sample JSON

```json
{
	"backupParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "23:00:00",
            "parameters": {
            	"days": [
                	"sunday",
                    "monday",
                    "tuesday",
                    "wednesday",
                    "thursday",
                    "friday",
                    "saturday"
                ]
            }
        },
        "backupName": "daily-backup-$(DATE)",
        "tags": [
        	{
            	"name": "Created by",
                "value": "Skeddly"
            }
        ]
    },
    "createdDate": "2016-06-08T15:14:00Z",
    "deleteBackupsParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "03:00:00",
            "parameters": {
            	"days": [
                	"saturday"
                ]
            }
        },
        "olderThanDays": 7,
        "minimumToKeep": 2,
        "isPerVolume": true
    },
    "isBackupInstance": true,
    "isDeleteBackups": true,
    "isStartInstance": true,
    "lastModifiedBy": "u-00000001",
    "managedInstanceGroupId": "mig-00000001",
    "name": "My Group",
    "startStopParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "08:00:00",
            "parameters": {
            	"days": [
                	"monday",
                    "tuesday",
                    "wednesday",
                    "thursday",
                    "friday"
                ]
            }
        },
        "stopTimeInSeconds": 43200
    },
    "timeZoneId": "UTC"
}
```

Specification for a Managed Instance Group.

Property | Type | Description
-------- | ---- | -----------
createdDate | string | Date, in ISO 8601 format, when the Managed Instance Group was created.
backupParameters | <a href="#managedinstancebackupparameters">object</a> | Parameters for the instance backup.
deleteBackupsParameters | <a href="#managedinstancedeletebackupsparameters">object</a> | Parameters for the instance backup deletions.
isBackupInstance | boolean | True if a backup schedule exists.
isDeleteBackups | boolean | True if a delete backups schedule exists.
isStartInstance | boolean | True if a start instance schedule exists.
managedInstanceGroupId | string | ID of the Managed Instance Group.
lastModifiedBy | string | ID of the user whom last modified the Managed Instance Group.
name | string | Name of the Managed Instance Group.
startStopParameters | <a href="#managedinstancestartstopparameters">object</a> | Parameters for starting and stopping the instance.
timeZoneId | string | ID of the time zone in which the Managed Instance Group will execute.

To check for the existance of a schedule, refer to the `isBackupInstance`, `isDeleteBackups`, and `isStartInstance` properties.

For performance reasons, `backupParameters`, `deleteBackupsParameters`, and `startStopParameters` will only be included when requested as part of the request.

## ManagedInstanceSchedule

> Sample JSON

```json
{
    "scheduleType": "daily",
    "timeOfDay": "23:00:00",
    "parameters": {
        "days": [
            "sunday",
            "monday",
            "tuesday",
            "wednesday",
            "thursday",
            "friday",
            "saturday"
        ]
    }
}
```

Specification for a Managed Instance schedule.

Property | Type | Description
-------- | ---- | -----------
scheduleType | string | Type of schedule. Valid values include: hourly, daily, monthly.
timeOfDay | string | Time of day to start. Format is 24-hour, "hh:mm:ss".
parameters | <a href="#scheduleparameters">object</a> | Extra parameters for the schedule.

## ManagedInstanceStartStopParameters

```json
{
	"schedule": {
    	"scheduleType": "daily",
        "timeOfDay": "08:00:00",
        "parameters": {
            "days": [
                "monday",
                "tuesday",
                "wednesday",
                "thursday",
                "friday"
            ]
        }
    },
    "stopTimeInSeconds": 43200
}
```

Specification for parameters specific to an instance start/stop schedule.

Property | Type | Description
-------- | ---- | -----------
schedule | <a href="#managedinstanceschedule">object</a> | Schedule for the deletion of backups.
stopTimeInSeconds | integer | Amount of time, in seconds, to keep the EC2 instance running.

## ManagedPolicy

```json
{
	"managedPolicyId": "full",
    "name": "Full Access"
}
```

Specification for a managed policy.

Property | Type | Description
-------- | ---- | -----------
managedPolicyId | string | ID of the managed policy.
name | string | Name of the managed policy.

## ModifyCredential

> Sample JSON for modifying an IAM role

```json
{
	"cloudProviderSubTypeId": "amazon-standard",
    "externalId": "skeddly-12345678",
    "name": "My Credentials",
    "roleArn": "arn:aws:iam:123456789012::role/Skeddly"
}
```

> Sample JSON for modifying an IAM access key

```json
{
	"accessKeyId": "AK123456789012345678",
	"cloudProviderSubTypeId": "amazon-standard",
    "name": "My Credentials",
    "secretAccessKey": "1234567890123456789012345678901234567890"
}
```

Specifies the credential information to modify.

Property | Type | Description
-------- | ---- | -----------
accessKeyId | string | Updated access key of the IAM user.
externalId | string | Updated external ID used with the IAM role. Must have been generated using <a href="#credentialsgenerateiamroleexternalid"></a>.
name | string | Updated friendly name for the credential.
roleArn | string | Updated ARN for the IAM role being registered.
secretAccessKey | string | Updated secret access key of the IAM user.

When modifying credentials, only the properties being modified need to be included.

## ModifyManagedInstanceGroup


> Sample JSON

```json
{
	"backupParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "23:00:00",
            "parameters": {
            	"days": [
                	"sunday",
                    "monday",
                    "tuesday",
                    "wednesday",
                    "thursday",
                    "friday",
                    "saturday"
                ]
            }
        },
        "backupName": "daily-backup-$(DATE)",
        "tags": [
        	{
            	"name": "Created by",
                "value": "Skeddly"
            }
        ]
    },
    "deleteBackupsParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "03:00:00",
            "parameters": {
            	"days": [
                	"saturday"
                ]
            }
        },
        "olderThanDays": 7,
        "minimumToKeep": 2,
        "isPerVolume": true
    },
    "name": "My Group",
    "startStopParameters": {
    	"schedule": {
        	"scheduleType": "daily",
            "timeOfDay": "08:00:00",
            "parameters": {
            	"days": [
                	"monday",
                    "tuesday",
                    "wednesday",
                    "thursday",
                    "friday"
                ]
            }
        },
        "stopTimeInSeconds": 43200
    },
    "timeZoneId": "UTC"
}
```

Specification for modifying an existing Managed Instance Group.

Property | Type | Description
-------- | ---- | -----------
backupParameters | <a href="#managedinstancebackupparameters">object</a> | Parameters for the instance backup.
deleteBackupsParameters | <a href="#managedinstancedeletebackupsparameters">object</a> | Parameters for the instance backup deletions.
name | string | Required. Name of the Managed Instance Group.
startStopParameters | <a href="#managedinstancestartstopparameters">object</a> | Parameters for starting and stopping the instance.
timeZoneId | string | Required. ID of the time zone in which the Managed Instance Group will execute.

## ModifyUser

```json
{
	"emailAddress": "user@example.com",
    "status": "enabled"
}
```

Updated values for an account sub-user.

Property | Type | Description
-------- | ---- | -----------
emailAddress | string | Updated email address for the user.
status | string | Updated status of the user. Valid values include: enabled, disabled.

## ModifyUserPassword

```json
{
	"password": "myreallystrongpassword"
}
```

New password to apply to a user.

Property | Type | Description
-------- | ---- | -----------
password | string | Updated password for the user.

## MonthlyScheduleParameters

> Sample JSON

```json
{
	"dayOfMonth": "indicate-day-and-week",
	"months": [
    	"january",
        "july"
    ],
    "weekAndDay": {
    	"day": "sunday",
        "week": "first"
    }
}
```

Parameters for a monthly schedule.

Derived from <a href="#scheduleparameters">ScheduleParameters</a> and includes all properties.

Property | Type | Description
-------- | ---- | -----------
dayOfMonth | string | Required. Day of the month to execute. Valid values include: same-day-as-start, indicate-day-and-week, last-day.
months | array of string | Required. Array of months of the year. Possible values include: january, february, march, april, may, june, july, august, september, october, november, december.
weekAndDay | <a href="#weekandday">object</a> | Conditional. Indicates the week and day to execute.

## NoneScheduleParameters

> Sample JSON

```json
{
}
```

Parameters for a "none" schedule.

Derived from <a href="#scheduleparameters">ScheduleParameters</a> and includes all properties.

## Region

> Sample JSON

```json
{
	"availabilityZones": [
    	"us-east-1a",
        "us-east-1b"
    ],
    "cloudProviderSubTypeId": "amazon-standard",
	"displayName": "N. Virginia",
    "regionName": "us-east-1"
}
```

Description of a region.

Property | Type | Description
-------- | ---- | -----------
availabilityZones | array of string | List of availability zones in the region.
cloudProviderSubTypeId | string | Cloud-provider sub-type for the region. Valid values include: amazon-stanard, amazon-govcloud-us, amazon-china.
displayName | string | Friendly name of the region.
regionName | string | System name of the region.

The `availabilityZones` property will only be populated when requested.

## RemoveUserMfa

> Sample JSON

```json
{
	"mfaType": "google-auth"
}
```

Parameters to remove MFA from an account sub-user.

Property | Type | Description
-------- | ---- | -----------
mfaType | array of string | Type of MFA to remove. Valid values include: google-auth, mobile-otp.

## ScheduleParameters

```json
{
}
```

Base model for the schedule parameter models:

* <a href="#nonescheduleparameters">NoneScheduleParameters</a>
* <a href="#hourlyscheduleparameters">HourlyScheduleParameters</a>
* <a href="#dailyscheduleparameters">DailyScheduleParameters</a>
* <a href="#weeklyscheduleparameters">WeeklyScheduleParameters</a>
* <a href="#monthlyscheduleparameters">MonthlyScheduleParameters</a>

## Tag

> Sample JSON

```json
{
	"name": "Tag name",
    "value": "Tag value"
}
```

Properties of a resource tag.

Property | Type | Description
-------- | ---- | -----------
name | string | Name of the tag.
value | string | Value of the tag.

## TimeZone

> Sample JSON

```json
{
	"displayName": "(UTC-5:00) Eastern Standard Time",
    "timeZoneId": "Eastern Standard Time"
}
```

Properties of a time zone.

Property | Type | Description
-------- | ---- | -----------
displayName | string | Name of the time zone.
timeZoneId | string | ID of the time zone.

## UpcomingActionExecution

> Sample JSON

```json
{
	"actionId": "a-00000001",
    "actionName": "My Action",
    "actionType": "amazon-start-ec2-instances",
    "actionVersionId": "av-00000001",
    "managedInstanceId": "mi-00000001",
    "startDate": "2016-06-09T10:57:00Z",
    "timeZoneId": "Eastern Standard Time"
}
```

Properties of a time zone.

Property | Type | Description
-------- | ---- | -----------
actionId | string | ID of the action.
actionName | string | Name of the action.
actionType | string | Type of action.
actionVersionId | string | Version ID of the action.
managedInstanceId | string | ID of the Managed Instance to which the action belongs.
startDate | string | Date, in ISO 8601 format, at which the action will next execute.
timeZoneId | string | Time zone in which the action will execute.

## User

> Sample JSON

```json
{
	"emailAddress": "user@example.com",
    "lastAccessDate": "2016-06-09T11:00:00Z",
    "managedPolicies": [
    	{
        	"managedPolicyId": "full",
    		"name": "Full Access"
        }
    ],
    "mfaType": "google-auth",
    "status": "enabled",
    "userId": "u-00000001",
    "username": "user1"
}
```

Properties of a time zone.

Property | Type | Description
-------- | ---- | -----------
emailAddress | string | Email address of the user.
lastAccessDate | string | Date, in ISO 8601 format, at which the user last signed-in.
managedPolicies | string | Managed policies attached to the user.
mfaType | string | Type of MFA device used by the user. Valid values include: none, google-auth, mobile-otp.
status | string | Status of the user. Valid values include: enabled, disabled, deleted.
userId | string | ID of the user.
username | string | Username of the user.

## WeekAndDay

> Sample JSON

```json
{
	"day": "sunday",
    "week": "first"
}
```

Indicator for a day in a month.

Property | Type | Description
-------- | ---- | -----------
day | string | Day of the week. Valid values include: sunday, monday, tuesday, wednesday, thursday, friday, saturday.
week | string | Week of the month. Valid values include: first, second, third, fourth, last.

## WeeklyScheduleParameters

> Sample JSON

```json
{
	"dayOfWeek": "same-day-as-start"
}
```

Parameters for a weekly schedule.

Derived from <a href="#scheduleparameters">ScheduleParameters</a> and includes all properties.

Property | Type | Description
-------- | ---- | -----------
dayOfWeek | string | Required. Day of the week to execute. Valid values include: same-day-as-start.
