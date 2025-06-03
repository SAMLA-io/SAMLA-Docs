Enables the creation of a new sparse Pinecone index for the SAMLA system. This endpoint establishes a foundational index that will be shared across all organizations, with each organization maintaining its own namespace within the index. The sparse index is optimized for efficient storage and retrieval of document embeddings, supporting the RAG system's core functionality.

- `POST /create-index`
    - Create a new Pinecone index
    - Parameters: 
        - `index_name`: Name of the Pinecone index
        - `region`: AWS region (default: "us-east-1")
            - Supported regions: us-east-1, us-west-2, eu-west-1
    - Creates index with multilingual-e5-large model and cosine similarity metric

    Example Request:
    ```bash
    curl -X POST "http://localhost:8000/create-index" \
         -H "Content-Type: application/json" \
         -d '{
           "index_name": "samla-enterprise",
           "region": "us-east-1"
         }'
    ```

    Example Response:
    ```json
    {
      "status": "success",
      "message": "Index 'samla-enterprise' created successfully",
      "index_name": "samla-enterprise"
    }
    ```
