Provides a comprehensive overview of all Pinecone indexes currently available in the SAMLA system. This endpoint enables administrators and system operators to monitor and manage the vector search infrastructure, ensuring proper resource allocation and maintenance.

- `GET /list-indexes`
    - List all Pinecone indexes in the SAMLA system
    - Returns array of index names

    Example Request:
    ```bash
    curl "http://localhost:8000/list-indexes"
    ```

    Example Response:
    ```json
    {
      "indexes": [
        "samla-enterprise",
        "samla-customer-1",
        "samla-customer-2"
      ]
    }
    ```