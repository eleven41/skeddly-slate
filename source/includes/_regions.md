# Regions

## List all regions

> Sample Request

```http
GET /api/Regions HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/Regions"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

```json
[
  {
    "availabilityZones": [
    	"us-east-1a",
        "us-east-1b"
    ],
    "cloudProviderSubTypeId": "amazon-standard",
    "displayName": "N. Virginia",
    "regionName": "us-east-1"
  }
]
```

Retrieves the list of regions.

### HTTP Request

`GET https://api.skeddly.com/api/Regions`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include | | Comma-separated list of extra data to include. Valid values include: availabilityZones.
cloudProviderId |  | Comma-separated list of cloud-providers. Valid values include: amazon.
cloudProviderSubTypeId | | Comma-separated list of cloud-provider sub-types. Valid values include: amazon-standard, amazon-govcloud-us, amazon-china.
credentialId | | ID of a credential.

<aside class="notice">
One of `cloudProviderId`, `cloudProviderSubTypeId`, or `credentialId` must be specified.
</aside>

### Returns

Array of [Region](#region) objects.

## Get a region

> Sample Request

```http
GET /api/Regions/us-east-1 HTTP/1.1
Host: api.skeddly.com
Authentication: AccessKey <api key>
```

```shell
curl "https://api.skeddly.com/api/Regions/us-east-1"
  -H "Authorization: AccessKey <api key>"
```

> Sample Response

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

Retrieves a single region.

### HTTP Request

`GET https://api.skeddly.com/api/Regions/<regionName>`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
regionName | | Region name of the region to retrieve.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include | | Comma-separated list of extra data to include. Valid values include: availabilityZones.

### Returns

A [Region](#region) object.
