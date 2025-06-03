Performs a powerful hybrid search, seamlessly blending both semantic and lexical search techniques across all indexes within your organization's Pinecone account. This dual approach harnesses the intelligence of semantic search—which interprets the meaning, context, and intent behind the query—alongside the precision of lexical search, which identifies exact keyword and phrase matches. By uniting these methods, the search delivers results that are not only comprehensive but also highly relevant, ensuring that no important document is overlooked.

- `GET /search`
    - Perform semantic search across organization's documents
    - Parameters: 
        - [[organization_id]]: The organization's unique identifier
        - `prompt`: The search query text
        - [[project_id]]: The project's unique identifier
    - Returns array of hits with:
        - `id`: Document identifier
        - `score`: Similarity score
        - `fields`: Document content and metadata

    Example Request:
    ```bash
    curl "http://localhost:8000/search?organization_id=org_123&prompt=What%20are%20the%20AI%20capabilities%3F&project_id=project_456"
    ```

    Example Response:
    ```json
    [
        {
          "id": "doc_789",
          "score": 0.92,
          "fields": {
            "content": "SAMLA's enterprise AI solution provides advanced natural language processing capabilities.",
            "project_id": "project_456",
            "title": "Product Overview",
            "author": "John Doe",
            "date": "2024-03-20"
          }
        },
        {
          "id": "doc_790",
          "score": 0.85,
          "fields": {
            "content": "The system includes machine learning models for text classification and sentiment analysis.",
            "project_id": "project_456",
            "title": "Technical Specifications",
            "author": "Jane Smith",
            "date": "2024-03-19"
          }
        }
    ]
    ```
    