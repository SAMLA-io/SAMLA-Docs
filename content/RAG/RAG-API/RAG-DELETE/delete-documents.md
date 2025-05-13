Allows organizations to securely delete specific documents from their namespace in the Pinecone index. This helps maintain clean data and comply with data retention requirements.

- `DELETE /delete-documents`
    - Removes specified documents from an organization's namespace in the Pinecone index.
    - Parameters:
        - [[organization_id]]: The unique identifier for your organization, ensuring that document deletion is securely scoped to your data and maintaining strict separation between different organizations' information.
        - `ids`: An array of document IDs to be deleted. Each ID must correspond to a document that exists within your organization's namespace.
    - Example Request:
        ```json
        {
            "organization_id": "acme-corp-123",
            "ids": [
                "doc-123",
                "doc-456",
                "doc-789"
            ]
        }
        ```
    - Returns a confirmation of the successful deletion operation
    - Example Response:
        ```json
        {
            "deleted_count": 2,
            "failed_ids": ["doc-789"]
        }
        ```