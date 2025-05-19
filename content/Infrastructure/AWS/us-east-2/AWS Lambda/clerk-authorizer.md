
Performs JWT Token verification using clerks's [`verifyToken`](https://clerk.com/docs/references/backend/verify-token) function, which is related to the SAMLA app in the Clerk Dashboard. This ensures that only JWT tokens which are issued by a signed clerk user and within a valid session are authorized to access our database. 
## Parameters
The parameters are automatically passed by API Gateway when performing API Calls, as this function works as an intermediate function between the user and the actual API Lambda function. Nevertheless, it requires the following parameters passed as part of the event: 

- `type`: 
- `authorizationToken`: 
- `methodArn`: 

## Returns
- A JSON Policy Document which is used by API Gateway to determine if the user has access to the resource. 

## Error Responses
- 401 Unauthorized: If the token is invalid or the user is not signed in
- 403 Forbidden: If the user does not have access to the resource
- 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

## Example Request
Calls to this lambda function are not direclty made by the user, but rather by API Gateway when performing a request to the actual Lambda function. 

## Example Response
```json
{
  "principalId": "1234567890",
  "policyDocument": {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Action": "execute-api:Invoke",
        "Effect": "Allow",
        "Resource": "arn:aws:execute-api:us-east-2:123456789012:1234567890/dev/GET/get-all"
      }
    ],
  },
  "context": {
    "stringKey": "string",
    "numberKey": "number",
    "booleanKey": "boolean"
  }
}

```

## Notes
- The JWT Token should be passed in the `Authorization` header of the request, with the format `Bearer <token>`.
- The JWT Token should be generated using the JWT Template defined in the Clerk Dashboard, via the `getToken` function, passing the `template` parameter.