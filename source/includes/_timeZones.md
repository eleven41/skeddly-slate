# Time Zones

## List all time zones

> Sample Request

```http
GET /api/TimeZones HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/TimeZones"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

```json
[
  {
    "displayName": "(UTC-5:00) Eastern Standard Time",
    "timeZoneId": "Eastern Standard Time"
  }
]
```

Retrieves the list of time zones.

### HTTP Request

`GET https://api.skeddly.com/api/TimeZones`

### Returns

Array of [TimeZone](#timezone) objects.

## Get a time zone

> Sample Request

```http
GET /api/TimeZones/Eastern%20Standard%20Time HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/TimeZones/Eastern%20Standard%20Time"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

```json
{
    "displayName": "(UTC-5:00) Eastern Standard Time",
    "timeZoneId": "Eastern Standard Time"
}
```

Retrieves a single time zone.

### HTTP Request

`GET https://api.skeddly.com/api/TimeZones/<timeZoneId>`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
timeZoneId | | ID of the time zone to retrieve.

<aside class="notice">Many time zone IDs have spaces and other characters not compatible with URL paths. Ensure to URL-encode the time zone ID.</aside>


### Returns

A [TimeZone](#timezone) object.
