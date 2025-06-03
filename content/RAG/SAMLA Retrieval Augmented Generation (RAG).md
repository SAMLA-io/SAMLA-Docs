# SAMLA RAG System

A powerful Retrieval-Augmented Generation (RAG) system designed for SAMLA's enterprise AI agents. This system enables efficient document retrieval and context-aware responses for enterprise customers.

## Overview

The SAMLA RAG system is built using FastAPI and Pinecone, providing a robust API for document management and semantic search capabilities. It supports multi-tenant architecture where each enterprise customer has their own isolated namespace within the system.

## Features

- **Multi-tenant Support**: Each enterprise customer has their own isolated namespace
- **Document Management**: Upload, delete, and manage documents securely
- **Semantic Search**: Advanced search capabilities using Pinecone's vector database with multilingual-e5-large model
- **RESTful API**: Clean and intuitive API endpoints for all operations
- **CORS Enabled**: Ready for integration with frontend applications

## Prerequisites

- Python 3.8+
- Pinecone API key
- Docker (optional, for containerized deployment)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/samla-io/rag.git
cd rag
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
Create a `.env` file with your Pinecone API key and both HOST names:
```
PINECONE_API_KEY=your_api_key_here
DENSE_HOST=your_dense_host_here
SPARSE_HOST=your_sparse_host_here
```

## Running the Application

### Local Development
```bash
uvicorn rag.app:app --host 0.0.0.0 --port 8000
```

### Docker Deployment
```bash
docker build -t samla-rag .
docker run -p 8000:8000 samla-rag
```

## API Endpoints

### Management Routes

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

### Search Routes

- `GET /search`
  - Perform semantic search across organization's documents
  - Parameters: 
    - `organization_id`: The organization's unique identifier
    - `prompt`: The search query text
    - `project_id`: The project's unique identifier
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

## Architecture

The system is built with the following components:
- FastAPI for the web framework
- Pinecone for vector database and semantic search
  - Uses multilingual-e5-large model for embeddings
  - Cosine similarity for distance metric
- Multi-tenant architecture with organization-based namespacing
- Project-based data classification within an organization
- RESTful API design with clear separation of concerns

## Security

- Each organization's data is isolated in its own namespace
- CORS middleware configured for secure cross-origin requests
- Environment variable-based configuration for sensitive data

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contributors

- [@jpgtzg](https://github.com/jpgtzg)
