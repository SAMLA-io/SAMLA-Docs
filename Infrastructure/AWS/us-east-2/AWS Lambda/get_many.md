: Retrieves multiple documents from a specified MongoDB collection based on a custom query. This endpoint provides flexible querying capabilities, allowing you to filter and retrieve specific documents that match your criteria.

- `GET /get_many`
    - Retrieves documents from a MongoDB collection based on a custom query.
    - Parameters:
        - `database`: The name of the MongoDB database containing the target collection. This parameter can be provided either in the query string or in the event object.
        - `collection`: The name of the collection from which to retrieve documents. This parameter can be provided either in the query string or in the event object.
        - `query`: A JSON string representing the MongoDB query criteria. This parameter can be provided either in the query string or in the event object.
    - Returns:
        - A JSON array containing all documents that match the query criteria, where each document includes:
            - All fields stored in the MongoDB document
            - ObjectId fields are automatically converted to strings for JSON compatibility
    - Error Responses:
        - 400 Bad Request: 
            - If the database, collection name, or query is missing
            - If the query parameter is not a valid JSON string
        - 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

Example Query:
```json
{
    "query": {
        "user_id": "1234567890"
    }
}

```

Example Response:
```json
[
    {
        "_id": "507f1f77bcf86cd799439011",
        "content": "Active document content",
        "status": "active",
        "created_at": "2024-03-20T10:00:00Z",
        "metadata": {
            "source": "user_upload"
        }
    },
    {
        "_id": "507f1f77bcf86cd799439012",
        "content": "Another active document",
        "status": "active",
        "created_at": "2024-03-20T11:00:00Z",
        "metadata": {
            "source": "api_import"
        }
    }
]
```

Note: The query parameter should be a valid MongoDB query in JSON format. You can use any valid MongoDB query operators such as `$gt`, `$lt`, `$in`, etc. The query will be executed as-is against the specified collection.