# Get All Documents

Retrieves all documents from a specified MongoDB collection within your organization's database. This endpoint provides a straightforward way to access the complete set of documents stored in a particular collection, making it ideal for scenarios where you need to view or process all available data.

## Endpoint Details
- **Endpoint:** `/get-all`
- **Method:** GET
- **Headers:**
  - `Content-Type: application/json`

## Parameters
- `database`: The name of the MongoDB database containing the target collection. This parameter can be provided either in the query string or in the request body.
- `collection`: The name of the collection from which to retrieve all documents. This parameter can be provided either in the query string or in the request body.

## Returns
- A JSON array containing all documents from the specified collection, where each document includes:
  - All fields stored in the MongoDB document
  - ObjectId fields are automatically converted to strings for JSON compatibility

## Error Responses
- 400 Bad Request: If the database or collection name is missing or invalid
- 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

## Example Request
```
GET /get-all?database=myDB&collection=users
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
curl -X GET \
  'https://your-api-url/get-all?database=myDB&collection=users' \
  -H 'Content-Type: application/json'
```

## Notes
- This endpoint returns all documents in the specified collection
- For large collections, consider using pagination or the get-many endpoint with specific filters
- All endpoints require proper authentication
- MongoDB connection string should be stored securely in environment variables
- Input validation is performed on all query parameters 