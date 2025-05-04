Retrieves a single document from a specified MongoDB collection based on a custom query. This endpoint is useful when you need to fetch a specific document that matches your criteria, and you expect only one result.

- `GET /get_one`
    - Retrieves a single document from a MongoDB collection based on a custom query.
    - Parameters:
        - `database`: The name of the MongoDB database containing the target collection. This parameter can be provided either in the query string or in the event object.
        - `collection`: The name of the collection from which to retrieve the document. This parameter can be provided either in the query string or in the event object.
        - `query`: A JSON string representing the MongoDB query criteria. This parameter can be provided either in the query string or in the event object.
    - Returns:
        - A single JSON object containing the document that matches the query criteria, including:
            - All fields stored in the MongoDB document
            - ObjectId fields are automatically converted to strings for JSON compatibility
    - Error Responses:
        - 400 Bad Request: 
            - If the database, collection name, or query is missing
            - If the query parameter is not a valid JSON string
        - 404 Not Found: If no document matches the query criteria
        - 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

Example Query:
```json
{
    "query": {
        "_id": "507f1f77bcf86cd799439011"
    }
}
```

Example Response:
```json
{
    "_id": "507f1f77bcf86cd799439011",
    "content": "Document content",
    "status": "active",
    "created_at": "2024-03-20T10:00:00Z",
    "metadata": {
        "source": "user_upload"
    }
}
```

Note: The query parameter should be a valid MongoDB query in JSON format. You can use any valid MongoDB query operators such as `$gt`, `$lt`, `$in`, etc. The query will be executed as-is against the specified collection. If multiple documents match the query criteria, only the first matching document will be returned.