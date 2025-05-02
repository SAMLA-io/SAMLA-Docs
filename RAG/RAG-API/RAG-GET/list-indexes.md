Provides a comprehensive overview of all Pinecone indexes currently available in the SAMLA system. This endpoint enables administrators and system operators to monitor and manage the vector search infrastructure, ensuring proper resource allocation and maintenance.

- `GET /list-indexes`
    - Retrieves a list of all Pinecone indexes configured for the SAMLA system.
    - No parameters required - this endpoint returns all indexes regardless of organization.
    - Returns an array of index objects, each containing:
        - `name`: The unique identifier of the index
        - `dimension`: The dimensionality of vectors stored in the index
        - `metric`: The similarity metric used by the index
        - `host`: The endpoint URL for the index
        - `status`: The current operational status of the index
    - Example Response:
        ```json
        {
            "indexes": [
                {
                    "name": "samla-dense-2024",
                    "dimension": 1536,
                    "metric": "cosine",
                    "host": "https://samla-dense-2024-xxxxx.svc.pinecone.io",
                    "status": "ready"
                },
                {
                    "name": "samla-sparse-2024",
                    "dimension": 1536,
                    "metric": "dotproduct",
                    "host": "https://samla-sparse-2024-xxxxx.svc.pinecone.io",
                    "status": "ready"
                }
            ]
        }
        ```