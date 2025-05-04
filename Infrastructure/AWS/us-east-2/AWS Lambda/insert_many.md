Inserts multiple documents into a specified MongoDB collection in a single operation. This endpoint is optimized for bulk document insertion, providing an efficient way to add multiple documents to your database at once.

- `POST /insert_many`
    - Inserts multiple documents into a MongoDB collection.
    - Parameters:
        - `database`: The name of the MongoDB database where documents will be inserted. This parameter can be provided either in the request body or in the query string.
        - `collection`: The name of the collection where documents will be inserted. This parameter can be provided either in the request body or in the query string.
        - `data`: A JSON array containing the documents to be inserted. This parameter can be provided either in the request body or in the query string.
    - Returns:
        - A JSON object containing:
            - `inserted_ids`: An array of string representations of the ObjectIds for the newly inserted documents
    - Error Responses:
        - 400 Bad Request: 
            - If the database, collection name, or data is missing
            - If the data parameter is not a valid JSON string
            - If the data is not an array of objects
        - 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

Example Request:
```json
{
    "database": "my_database",
    "collection": "my_collection",
    "data": [
        {
            "content": "First document content",
            "status": "active",
            "created_at": "2024-03-20T10:00:00Z",
            "metadata": {
                "source": "user_upload"
            }
        },
        {
            "content": "Second document content",
            "status": "active",
            "created_at": "2024-03-20T11:00:00Z",
            "metadata": {
                "source": "api_import"
            }
        }
    ]
}
```

Example Response:
```json
{
    "inserted_ids": [
        "507f1f77bcf86cd799439011",
        "507f1f77bcf86cd799439012"
    ]
}
```

Note: The data parameter must be a JSON array containing objects to be inserted. Each object in the array will be inserted as a separate document in the collection. If you don't provide an `_id` field in your documents, MongoDB will automatically generate one for each document.