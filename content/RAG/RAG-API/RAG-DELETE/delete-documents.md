Allows organizations to securely delete specific documents from their namespace in the Pinecone index. This helps maintain clean data and comply with data retention requirements.

- `DELETE /delete-documents`
    - Delete documents from an organization's namespace
    - Request body:
        ```json
        {
          "organization_id": "string",
          "ids": ["string"]
        }
        ```

    Example Request:
    ```bash
    curl -X DELETE "http://localhost:8000/delete-documents" \
         -H "Content-Type: application/json" \
         -d '{
           "organization_id": "org_123",
           "ids": ["doc_789", "doc_790"]
         }'
    ```

    Example Response:
    ```json
    {
      "status": "success",
      "message": "Documents deleted successfully",
      "deleted_count": 2
    }
    ```