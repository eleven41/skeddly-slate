# Actions

## List all actions

> Sample Request

```http
GET /api/Actions HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/Actions"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

```json
[
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
]
```

Retrieves the list of actions.

### HTTP Request

`GET https://api.skeddly.com/api/Actions`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include |  | A comma-separated list of extra data to include. Valid values include: displayData, lastExecution, parameters, runningCount.
filter.actionClasses |  | A comma-separated list of types of actions. Value values include: standard, managedInstances.
filter.actionTypes | | A comma-separated list of action types.
filter.credentialIds |  | A comma-separated list of credential IDs.
filter.isEnabled |  | True or false.
filter.managedInstanceIds | | Comma-separated list of Managed Instance IDs.
filter.regions | | Comma-separated list of region system names.
filter.tags | | comma-separated list of tags.
filter.tagsRequired | any | Indicates whether all tags are required. Valid values include: any, all.

### Returns

Array of <a href="#action">Action</a> objects.

## Get an action

> Sample Request

```http
GET /api/Actions/a-00000001 HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/Actions/a-00000001"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

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

Retrieves the latest version of an action, or a specific version of an action.

### HTTP Request

`GET https://api.skeddly.com/api/Actions/<id>`

### URL Parameters

Parameter | Description
--------- | -----------
id | ID of the action or action version.

When specifying an action ID for `id`, the latest version of the action will be returned. When specifying an action version ID for `id`, the specified version will be returned.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include |  | A comma-separated list of extra data to include. Valid values include: displayData, lastExecution, parameters.

### Returns

An <a href="#action">Action</a> object.

## Execute an action

> Sample Request

```http
PUT /api/Actions/ae-00000001/Execute HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl -X PUT "https://api.skeddly.com/api/Actions/ae-00000001/Execute"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

```json
{
    "actionExecutionId": "ae-00000001",
    "status": "running",
    "startDate": "2016-06-01T12:00:00Z",
    "trigger": "user",
    "actionId": "a-00000001",
    "actionVersionId": "av-00000001",
    "actionType": "amazon-start-ec2-instance",
    "actionName": "Start My Instances",
    "timeZoneId": "UTC",
    "credentialId": "cred-00000001"
}
```

Executes an existing action. The action must be enabled.

### HTTP Request

`PUT https://api.skeddly.com/api/Actions/<id>/Execute`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the action.

### Returns

An [ActionExecution](#actionexecution) object.

