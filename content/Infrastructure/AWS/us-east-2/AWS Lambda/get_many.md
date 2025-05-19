# Get Many Documents

Retrieves multiple documents from a specified MongoDB collection based on a custom query. This endpoint provides flexible querying capabilities, allowing you to filter and retrieve specific documents that match your criteria.
## Parameters
- `database`: The name of the MongoDB database containing the target collection. This parameter can be provided either in the request body or in the query string.
- `collection`: The name of the collection from which to retrieve documents. This parameter can be provided either in the request body or in the query string.
- `query`: A JSON object representing the MongoDB query criteria. This parameter can be provided either in the request body or in the query string.

## Returns
- A JSON array containing all documents that match the query criteria, where each document includes:
  - All fields stored in the MongoDB document
  - ObjectId fields are automatically converted to strings for JSON compatibility

## Error Responses
- 400 Bad Request: 
  - If the database, collection name, or query is missing
  - If the query parameter is not a valid JSON string
- 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

## Example Request
```json
{
    "database": "myDB",
    "collection": "users",
    "query": {
        "age": {"$gt": 18}
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
    "body": [
        {
            "_id": "507f1f77bcf86cd799439011",
            "name": "John",
            "age": 25,
            "email": "john@example.com"
        },
        {
            "_id": "507f1f77bcf86cd799439012",
            "name": "Jane",
            "age": 30,
            "email": "jane@example.com"
        }
    ]
}
```

## Example using curl
```bash
curl -X POST \
  https://your-api-url/get-many \
  -H 'Content-Type: application/json' \
  -d '{
    "database": "myDB",
    "collection": "users",
    "query": {
        "age": {"$gt": 18}
    }
}'
```

## Notes
- The query parameter should be a valid MongoDB query in JSON format
- You can use any valid MongoDB query operators such as `$gt`, `$lt`, `$in`, etc.
- All endpoints require proper authentication
- MongoDB connection string should be stored securely in environment variables
- Input validation is performed on all query parameters