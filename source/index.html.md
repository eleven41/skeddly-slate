---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Skeddly API.

# Making Requests

All API requests must be made to the following endpoint:

`https://api.skeddly.com/api/`

All requests must use HTTPS.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: AccessKey s<api key>"
```

> Make sure to replace `<api key>` with your API key.

In order to use the Skeddly API, you require an API key. API keys can be obtained by doin the following:

1. Sign-in to your Skeddly account.
2. Click your username on the top-right of the page, then click "Account Settings".
3. Scroll down to the "API Key Management" section, and click "Manage API Keys".
4. Click the "Create API Key" button to create an API key.

When making HTTP requests, all requests must include the "Authorization:" header in the following format:

`Authorization: AccessKey <api key>`

<aside class="notice">
You must replace <code>&lt;api key&gt;</code> with your personal API key.
</aside>

# Action Executions

## List all action executions

> Example Request

```shell
curl "https://api.skeddly.com/api/ActionExecutions"
  -H "Authorization: AccessKey <api key>"
```

> Example Response

```json
[
  {
    "actionExecutionId": "ae-00000001",
    "status": "complete",
    "startDate": "2016-06-01T12:00:00Z",
    "endDate": "2016-06-01T12:03:00Z",
    "result": {
    	"code": 0,
        "text": "Execution succeeded"
    },
    "trigger": "schedlue",
    "actionId": "a-00000001",
    "actionVersionId": "av-00000001",
    "actionType": "amazon-start-ec2-instance",
    "actionName": "Start My Instances",
    "timeZoneId": "UTC",
    "credentialId": "cred-00000001"
  }
]
```

Retrieves the list of action executions.

### HTTP Request

`GET https://api.skeddly.com/api/ActionExecutions`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include |  | A comma-separated list of extra extra data to include.
filter.status | all | Execution status to limit results. Valid values include: all, errorsOnly, completedOnly, runningOnly.
filter.actionIds |  | A comma-separated list of action IDs.
filter.credentialIds |  | A comma-separated list of credential IDs.
filter.actionClasses |  | A comma-separated list of types of actions for which to include executions. Value values include: standard, managedInstances.
filter.dateComparesTo | startDate | Indicator to which the date range references. Value values include: startDate, endDate.
filter.range.inclusiveStart | now - 30 days | Start date (inclusive) of the date range, in ISO8601 format.
filter.range.exclusiveEnd | now | End date (exclusive) of the date range, in ISO8601 format.

### Returns

Array of <a href="#actionexecution">ActionExecution</a> objects.

## Get an action execution

> Example Request

```shell
curl "https://api.skeddly.com/api/ActionExecutions/ae-00000001"
  -H "Authorization: AccessKey <api key>"
```

> Example Response

```json
{
    "actionExecutionId": "ae-00000001",
    "status": "complete",
    "startDate": "2016-06-01T12:00:00Z",
    "endDate": "2016-06-01T12:03:00Z",
    "result": {
        "code": 0,
        "text": "Execution succeeded"
    },
    "trigger": "schedlue",
    "actionId": "a-00000001",
    "actionVersionId": "av-00000001",
    "actionType": "amazon-start-ec2-instance",
    "actionName": "Start My Instances",
    "timeZoneId": "UTC",
    "credentialId": "cred-00000001"
}
```

Retrieves information about a single action execution.

### HTTP Request

`GET https://api.skeddly.com/api/ActionExecutions/<id>`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the action exection.

### Returns

An <a href="#actionexecution">ActionExecution</a> object.

## Cancel an action execution

> Example Request

```shell
curl -X PUT "https://api.skeddly.com/api/ActionExecutions/ae-00000001/Cancel"
  -H "Authorization: AccessKey <api key>"
```

> Example Response

```json
{
    "actionExecutionId": "ae-00000001",
    "status": "cancelling",
    "startDate": "2016-06-01T12:00:00Z",
    "trigger": "schedlue",
    "actionId": "a-00000001",
    "actionVersionId": "av-00000001",
    "actionType": "amazon-start-ec2-instance",
    "actionName": "Start My Instances",
    "timeZoneId": "UTC",
    "credentialId": "cred-00000001"
}
```

Cancels a running action execution. The action will stop and execute any
cancelling logic.

### HTTP Request

`PUT https://api.skeddly.com/api/ActionExecutions/<id>/Cancel`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the action exection.

### Returns

An <a href="#actionexecution">ActionExecution</a> object.

# Models

## Action

> Sample JSON

```json
{
    "actionId": "a-00000001",
    "actionType": "amazon-start-ec2-instance",
    "actionVersionId": "av-00000001",
    "credentialId": "cred-00000001",
    "isEnabled": true,
    "lastModifiedBy": "u-000000001",
    "lastModifiedDate": "2016-06-07T19:58:00Z",
    "name": "Start My Instances",
    "timeZoneId": "UTC"
}
```

Represents an action.

Property | Type | Description
-------- | ---- | -----------
actionId | string | ID of the action.
actionType | string | Type ID of the action.
actionVersionId | string | Version ID of the action.
credentialId | string | ID of the credential.
isEnabled | boolean | True if the action is enabled to execute. False otherwise.
lastModifiedBy | string | ID of the user whom last modified the action.
lastModifiedDate | string | Date, in ISO 8601 format, at which the action was last modified.
name | string | Name of the action.
timeZoneId | string | ID of the time zone for the action.

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
    "trigger": "schedlue"
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
result | object | Will not be present if the status is not "complete".
startDate | string | Date, in ISO8601 format, when the action started.
status | string | Status of the execution. Valid values include: running, complete, cancelling.
timeZoneId | string | ID of the time zone for the action.
trigger | string | Trigger which started the action. Valid values include: schedule, user, sns.

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

# API Clients

## Official

The following clients are officially supported by the Skeddly team.

* [https://github.com/eleven41/skeddly-sdk-net](https://github.com/eleven41/skeddly-sdk-net) - .NET