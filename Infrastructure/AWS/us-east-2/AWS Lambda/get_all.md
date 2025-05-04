Retrieves all documents from a specified MongoDB collection within your organization's database. This endpoint provides a straightforward way to access the complete set of documents stored in a particular collection, making it ideal for scenarios where you need to view or process all available data.

- `GET /get_all`
    - Retrieves all documents from a specified MongoDB collection.
    - Parameters:
        - `database`: The name of the MongoDB database containing the target collection. This parameter can be provided either in the query string or in the event object.
        - `collection`: The name of the collection from which to retrieve all documents. This parameter can be provided either in the query string or in the event object.
    - Returns:
        - A JSON array containing all documents from the specified collection, where each document includes:
            - All fields stored in the MongoDB document
            - ObjectId fields are automatically converted to strings for JSON compatibility
    - Error Responses:
        - 400 Bad Request: If the database or collection name is missing or invalid
        - 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

Example Response:
```json
[
    {
        "_id": "507f1f77bcf86cd799439011",
        "content": "Sample document content",
        "metadata": {
            "created_at": "2024-03-20T10:00:00Z",
            "source": "user_upload"
        }
    },
    {
        "_id": "507f1f77bcf86cd799439012",
        "content": "Another document",
        "metadata": {
            "created_at": "2024-03-20T11:00:00Z",
            "source": "api_import"
        }
    }
]
``` 