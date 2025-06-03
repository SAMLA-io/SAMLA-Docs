Enables seamless document ingestion by allowing you to upload one or multiple documents directly into your organization's namespace within Pinecone. This endpoint is designed for flexibility, supporting not only the core content of each document but also any additional metadata you wish to associate—such as source, author, or custom tags. By centralizing document uploads, you ensure that all relevant information is securely stored and immediately available for future search and retrieval operations.

- `POST /upload-documents`
    - Upload documents to an organization's namespace
    - Request body:
        ```json
        {
          "organization_id": "string",
          "documents": [
            {
              "content": "string",
              ...additional_metadata
            }
          ]
        }
        ```
    - Make sure to include a `project_id` field in the metadata for each document, this will be used to identify the project the document belongs to within the organization. If the information related to general information about the organization, use "general" as the project_id.
    - Returns count of uploaded documents

    Example Request:
    ```bash
    curl -X POST "http://localhost:8000/upload-documents" \
         -H "Content-Type: application/json" \
         -d '{
           "organization_id": "org_123",
           "documents": [
             {
               "content": "SAMLA's enterprise AI solution provides advanced natural language processing capabilities.",
               "project_id": "project_456",
               "title": "Product Overview",
               "author": "John Doe",
               "date": "2024-03-20"
             },
             {
               "content": "General company information and policies.",
               "project_id": "general",
               "title": "Company Policies",
               "author": "HR Department",
               "date": "2024-03-19"
             }
           ]
         }'
    ```

    Example Response:
    ```json
    {
      "status": "success",
      "message": "Documents uploaded successfully",
      "uploaded_count": 2
    }
    ```