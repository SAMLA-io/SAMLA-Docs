Inserts a single document into a specified MongoDB collection. This endpoint is designed for inserting individual documents and provides a simple way to add new data to your database.

- `POST /insert_one`
    - Inserts a single document into a MongoDB collection.
    - Parameters:
        - `database`: The name of the MongoDB database where the document will be inserted. This parameter can be provided either in the request body or in the query string.
        - `collection`: The name of the collection where the document will be inserted. This parameter can be provided either in the request body or in the query string.
        - `data`: A JSON object containing the document to be inserted. This parameter can be provided either in the request body or in the query string.
    - Returns:
        - A JSON object containing:
            - `Object inserted with inserted_id`: A string representation of the ObjectId for the newly inserted document
    - Error Responses:
        - 400 Bad Request: 
            - If the database, collection name, or data is missing
            - If the data parameter is not a valid JSON string
        - 500 Internal Server Error: If there's an issue connecting to MongoDB or processing the request

Example Request:
```json
{
    "database": "my_database",
    "collection": "my_collection",
    "data": {
        "content": "Document content",
        "status": "active",
        "created_at": "2024-03-20T10:00:00Z",
        "metadata": {
            "source": "user_upload"
        }
    }
}
```

Example Response:
```json
{
    "Object inserted with inserted_id": "507f1f77bcf86cd799439011"
}
```

Note: The data parameter must be a valid JSON object. If you don't provide an `_id` field in your document, MongoDB will automatically generate one. The response will include the generated or provided `_id` as a string.