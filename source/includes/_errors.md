# Errors

When errors occur, the Skeddly API will return a JSON structure with the following properties:

```json
{
	"errorCode": "UnauthorizedOperation",
    "message": "You are not authorized to execute actions:ListActions"
}
```

Property | Description
-------- | -----------
errorCode | <a href="#errorcodes">Error code</a> related to the error.
message | Descriptive message explaining (as best as possible) the error.