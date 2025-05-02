Enables seamless document ingestion by allowing you to upload one or multiple documents directly into your organization’s namespace within Pinecone. This endpoint is designed for flexibility, supporting not only the core content of each document but also any additional metadata you wish to associate—such as source, author, or custom tags. By centralizing document uploads, you ensure that all relevant information is securely stored and immediately available for future search and retrieval operations.

- `POST /upload-documents`
    - Uploads new documents to your organization’s namespace, making them available for search and analysis.
    - Parameters:
        - [[organization_id]]: The unique identifier for your organization, ensuring that uploaded documents are securely scoped to your data and maintaining strict separation between different organizations’ information.
        - `documents`: An array of document objects to be uploaded. Each object must include:
            - `content`: The main text or body of the document. This can be anything from a meeting transcript to a technical report.
            - ...additional_metadata: Optional fields such as `source`, `author`, `timestamp`, or any custom metadata relevant to your use case. These fields enhance document discoverability and context during search.
    - Returns the count of successfully uploaded documents, confirming that your data is now available for search and retrieval.
        - Example:
			```json
			{
			  "organization_id": "acme-corp-123",
			  "documents": [
				{
				  "content": "Q3 marketing strategy outcomes were positive...",
				  "source": "internal report",
				  "author": "Jane Doe",
				  "created_at": "2024-06-01"
				},
				{
				  "content": "Customer feedback summary for May...",
				  "source": "survey",
				  "tags": ["customer", "feedback", "2024"]
				}
			  ]
			}
			```