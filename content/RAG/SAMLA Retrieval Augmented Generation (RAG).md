
A powerful [Retrieval-Augmented Generation](https://github.com/SAMLA-io/RAG) system designed for SAMLA's enterprise AI agents. This system enables efficient document retrieval and context-aware responses for enterprise customers.

## Overview

The SAMLA RAG system is built using FastAPI and Pinecone, providing a robust API for document management and semantic search capabilities. It supports multi-tenant architecture where each enterprise customer has their own isolated namespace within the system.

## Features

- **Multi-tenant Support**: Each enterprise customer has their own isolated namespace
- **Document Management**: Upload, delete, and manage documents securely
- **Semantic Search**: Advanced search capabilities using Pinecone's vector database with multilingual-e5-large model
- **RESTful API**: Clean and intuitive API endpoints for all operations
- **CORS Enabled**: Ready for integration with frontend applications

## API Endpoints
- [[search]]
- [[create-dense-index]]
- [[create-sparse-index]]
- [[list-indexes]]
- [[upload-documents]]
- [[delete-documents]]
