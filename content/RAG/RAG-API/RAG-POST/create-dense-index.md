Enables the creation of a new dense Pinecone index for the SAMLA system. This endpoint establishes a high-dimensional vector index that will be shared across all organizations, with each organization maintaining its own namespace within the index. The dense index is optimized for semantic search and similarity matching, supporting the RAG system's ability to find contextually relevant documents.

- `POST /create-dense-index`
    - Creates a new dense Pinecone index that will be used by the entire SAMLA system.
    - Parameters:
        - `index_name`: The unique identifier for the new Pinecone index. This name will be used to reference the index in subsequent operations.
        - `region`: The AWS region where the index will be hosted. This parameter ensures optimal performance and compliance with data residency requirements.
            - Supported regions:
                - `us-east-1`: North Virginia (default)
                - `us-west-2`: Oregon
                - `eu-west-1`: Ireland
    - Returns a confirmation of the successful index creation or an error message if the operation fails.
    - Example:
        ```json
        {
            "index_name": "samla-dense-2024",
            "region": "us-east-1"
        }
        ```