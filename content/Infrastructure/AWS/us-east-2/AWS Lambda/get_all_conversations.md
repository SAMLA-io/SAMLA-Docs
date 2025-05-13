# Get All Conversations

Retrieves all conversations from a specified MongoDB collection. This endpoint is specifically designed to fetch conversation data, providing a comprehensive view of all conversations stored in the database.

## Endpoint Details
- **Endpoint:** `/get-all-conversations`
- **Method:** GET
- **Headers:**
  - `Content-Type: application/json`

## Parameters
- `organization_id`: The name of the MongoDB database (organization_id) containing the conversations collection. This parameter can be provided either in the query string or in the request body.
- `user_id`: Filter conversations by user ID to only return conversations where this user is a participant. This parameter can be provided either in the query string or in the request body.

## Returns
- A JSON array containing all conversations from the specified collection, where each conversation includes:
  - All fields stored in the MongoDB document
  - ObjectId fields are automatically converted to strings for JSON compatibility
  - Conversation-specific fields such as messages, participants, timestamps, etc.

## Error Responses
- 400 Bad Request: If the database or collection name is missing or invalid
- 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

## Example Request
```
GET /get-all-conversations?database=myDB&collection=conversations
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
            "participants": ["user1", "user2"],
            "messages": [
                {
                    "sender": "user1",
                    "content": "Hello!",
                    "timestamp": "2024-03-20T10:00:00Z"
                },
                {
                    "sender": "user2",
                    "content": "Hi there!",
                    "timestamp": "2024-03-20T10:01:00Z"
                }
            ],
            "created_at": "2024-03-20T10:00:00Z",
            "last_updated": "2024-03-20T10:01:00Z"
        },
        {
            "_id": "507f1f77bcf86cd799439012",
            "participants": ["user1", "user3"],
            "messages": [
                {
                    "sender": "user1",
                    "content": "How are you?",
                    "timestamp": "2024-03-20T11:00:00Z"
                }
            ],
            "created_at": "2024-03-20T11:00:00Z",
            "last_updated": "2024-03-20T11:00:00Z"
        }
    ]
}
```

## Example using curl
```bash
curl -X GET \
  'https://your-api-url/get-all-conversations?database=myDB&collection=conversations' \
  -H 'Content-Type: application/json'
```

## Notes
- This endpoint returns all conversations in the specified collection
- For large collections, consider using pagination or implementing filters
- Conversations are returned in chronological order based on creation time
- All endpoints require proper authentication
- MongoDB connection string should be stored securely in environment variables
- Input validation is performed on all query parameters