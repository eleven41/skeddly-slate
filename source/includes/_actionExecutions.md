# Action Executions

## List all action executions

> Sample Request

```http
GET /api/ActionExecutions HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/ActionExecutions"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

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
    "trigger": "schedule",
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

> Sample Request

```http
GET /api/ActionExecutions/ActionExecutions/ae-00000001 HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/ActionExecutions/ae-00000001"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

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
    "trigger": "schedule",
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

> Sample Request

```http
PUT /api/ActionExecutions/ae-00000001/Cancel HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl -X PUT "https://api.skeddly.com/api/ActionExecutions/ae-00000001/Cancel"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

```json
{
    "actionExecutionId": "ae-00000001",
    "status": "cancelling",
    "startDate": "2016-06-01T12:00:00Z",
    "trigger": "schedule",
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

## List all upcoming action executions

> Sample Request

```http
GET /api/ActionExecutions/Upcoming HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/ActionExecutions/Upcoming"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

```json
[
  {
    "actionId": "a-00000001",
    "actionName": "Start My Instances",
    "actionType": "amazon-start-ec2-instance",
    "actionVersionId": "av-00000001",
    "managedInstanceId": "mi-00000001",
    "startDate": "2016-06-09T12:41:00Z",
    "timeZoneId": "UTC"
  }
]
```

Retrieves the list of upcoming action executions.

### HTTP Request

`GET https://api.skeddly.com/api/ActionExecutions/Upcoming`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
filter.actionClasses |  | A comma-separated list of types of actions. Value values include: standard, managedInstances.

### Returns

Array of [UpcomingActionExecution](#upcomingactionexecution) objects.

