# Error Codes

The Skeddly API will use the following error codes within the JSON to indicate errors in the API operation.

Error Code | Meaning
---------- | -------
ActionExecutionNotFound | The specified action execution cannot be not found.
ActionCannotBeDeleted | The specified action cannot be deleted.
ActionNotFound | The specified action cannot be found.
CredentialInUse | The specified credential is in use.
CredentialNotFound | The specified credential cannot found found.
ErrorChangingPassword | An error occurred changing the user password.
InvalidActionExecutionId | The specified action execution ID is invalid.
InvalidActionId | The specified action ID is invalid.
InvalidActionVersionId | The specified action version ID is invalid.
InvalidCredentialId | The specified credential ID is invalid.
InvalidManagedInstanceId | The specified Managed Instance ID is invalid.
InvalidParameter | One of the parameters in the request is invalid.
InvalidRequest | The request is invalid.
InvalidRoleOrAccessDenied | The specified IAM role is invalid, or it could not be assumed.
InvoiceNotFound | The specified invoice cannot be found.
ManagedInstanceGroupNotFound | The specified Managed Instance Group cannot be found.
ManagedPolicyNotFound | The specified managed policy cannot be found.
TimeZoneNotFound | The specified time zone cannot be found.
UnauthorizedOperation | The caller is not authorized to execute the command.
UserNotFound | The specified user cannot be found.