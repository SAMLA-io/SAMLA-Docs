# Amazon API Gateway

Amazon API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. 

APIs act as the "front door" for applications to access data, business logic, or functionality from your backend services.

All API calls are authenticated, view [[Authentication]] for further information.

## API Endpoints

### GET Endpoints

#### Get All Documents
- **Endpoint:** `/get-all`
- **Method:** GET
- **Parameters (URL):**
  - `database`: The name of the MongoDB database
  - `collection`: The name of the collection to query
- **Description:** Retrieves all documents from a specified collection. See [[get_all]] for more details.

#### Get All Conversations
- **Endpoint:** `/get-all-conversations`
- **Method:** GET
- **Parameters (URL):**
  - `organization_id`: The name of the MongoDB database (organization_id)
  - `user_id`: (Optional) Filter conversations by user ID
- **Description:** Retrieves all conversations from a specified collection. See [[get_all_conversations]] for more details.

### POST Endpoints

#### Get One Document
- **Endpoint:** `/get-one`
- **Method:** POST
- **Parameters (Body):**
  ```json
  {
    "database": "string",
    "collection": "string",
    "query": {
      // MongoDB query object
    }
  }
  ```
- **Description:** Retrieves a single document based on query criteria. See [[get_one]] for more details.

#### Get Many Documents
- **Endpoint:** `/get-many`
- **Method:** POST
- **Parameters (Body):**
  ```json
  {
    "database": "string",
    "collection": "string",
    "query": {
      // MongoDB query object
    }
  }
  ```
- **Description:** Retrieves multiple documents based on query criteria. See [[get_many]] for more details.

#### Insert One Document
- **Endpoint:** `/insert-one`
- **Method:** POST
- **Parameters (Body):**
  ```json
  {
    "database": "string",
    "collection": "string",
    "data": {
      // Document to insert
    }
  }
  ```
- **Description:** Inserts a single document into a collection. See [[insert_one]] for more details.

#### Insert Many Documents
- **Endpoint:** `/insert-many`
- **Method:** POST
- **Parameters (Body):**
  ```json
  {
    "database": "string",
    "collection": "string",
    "data": [
      // Array of documents to insert
    ]
  }
  ```
- **Description:** Inserts multiple documents into a collection. See [[insert_many]] for more details.

## Common Response Format

All endpoints return responses in the following format:

```json
{
    "statusCode": number,
    "headers": {
        "Content-Type": "application/json"
    },
    "body": {
        // Response data
    }
}
```

## Error Responses

All endpoints may return the following error responses:

- **400 Bad Request:** Invalid parameters or request format
- **404 Not Found:** Resource not found (for get-one endpoint)
- **500 Internal Server Error:** Server-side error

## Notes

- All endpoints are currently configured without authorization for debugging purposes
- MongoDB connection strings are stored securely in environment variables
- Input validation is performed on all parameters
- ObjectId fields are automatically converted to strings in responses
- For large collections, consider using pagination or specific filters

