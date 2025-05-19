Authentication for all API calls via API Gateway (which should and currently are the only way of accessing SAMLA information) is done by passing a JWT Token related to the current Clerk Session ID (of a signed user) 

When performing an API call, the Clerk JWT Token should be passed in the `Authorization` header of the request, with the format `Bearer <token>`.

The authorization process is done by the `clerk-authorizer` Lambda function, which is triggered by API Gateway and is responsible for verifying the JWT Token and returning a policy document to API Gateway, which is used to determine if the user has access to the resource.
