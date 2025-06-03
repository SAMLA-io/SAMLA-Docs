Enables the creation of a new dense Pinecone index for the SAMLA system. This endpoint establishes a high-dimensional vector index that will be shared across all organizations, with each organization maintaining its own namespace within the index. The dense index is optimized for semantic search and similarity matching, supporting the RAG system's ability to find contextually relevant documents.

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