# Get One Document

Retrieves a single document from a specified MongoDB collection based on a custom query. This endpoint is useful when you need to fetch a specific document that matches your criteria, and you expect only one result.
## Parameters
- `database`: The name of the MongoDB database containing the target collection. This parameter can be provided either in the request body or in the query string.
- `collection`: The name of the collection from which to retrieve the document. This parameter can be provided either in the request body or in the query string.
- `query`: A JSON object representing the MongoDB query criteria. This parameter can be provided either in the request body or in the query string.

## Returns
        - A single JSON object containing the document that matches the query criteria, including:
            - All fields stored in the MongoDB document
            - ObjectId fields are automatically converted to strings for JSON compatibility

## Error Responses
        - 400 Bad Request: 
            - If the database, collection name, or query is missing
            - If the query parameter is not a valid JSON string
        - 404 Not Found: If no document matches the query criteria
        - 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

## Example Request
```json
{
    "database": "myDB",
    "collection": "users",
    "query": {
        "name": "John"
    }
}
```

## Example Response
```json
{
    "statusCode": 200,
    "headers": {
        "Content-Type": "application/json"
    },
    "body": {
    "_id": "507f1f77bcf86cd799439011",
        "name": "John",
        "age": 25,
        "email": "john@example.com"
    }
}
```

## Example using curl
```bash
curl -X POST \
  https://your-api-url/get-one \
  -H 'Content-Type: application/json' \
  -d '{
    "database": "myDB",
    "collection": "users",
    "query": {
        "name": "John"
    }
}'
```

## Notes
- The query parameter should be a valid MongoDB query in JSON format
- You can use any valid MongoDB query operators such as `$gt`, `$lt`, `$in`, etc.
- If multiple documents match the query criteria, only the first matching document will be returned
- All endpoints require proper authentication
- MongoDB connection string should be stored securely in environment variables
- Input validation is performed on all query parameters
Note: The query parameter should be a valid MongoDB query in JSON format. You can use any valid MongoDB query operators such as `$gt`, `$lt`, `$in`, etc. The query will be executed as-is against the specified collection. If multiple documents match the query criteria, only the first matching document will be returned.