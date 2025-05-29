> Samuel is SAMLA's intelligent analyst who monitors key business metrics, analyzes operational data in real time, and proposes decisions to optimize processes. He helps companies understand what is working, identify bottlenecks, and take informed actions based on evidence, not assumptions. With his capabilities, he improves efficiency, reduces costs, and accelerates growth by turning data into strategies.

Samuel is a multi-model agent that uses GPT-4, GPT-4 Optimized, and GPT-3.5 Turbo. It also uses the [[SAMLA Retrieval Augmented Generation (RAG)]] as an additional context source. Configuration for Samuel is done via the `avilable_agents` collection in MongoDB for each organization. 

Samuel retrieves context from the [[SAMLA Retrieval Augmented Generation (RAG)]] system, and makes uses of [[AWS Lambda]] functions to connect to MongoDB for storing and retrieving chat history and session data. This ensures secure and reliable data management for all interactions.
## Technical Integration

### Environment Setup

Required environment variables:
```
OPENAI_API_KEY=your_openai_api_key
RAG_URL=your_rag_service_url
MONGO_AWS_URL=your_mongo_url
MONGO_AWS_TOKEN=your_mongo_token
MONGO_CHAT_HISTORY_COLLECTION=your_collection_name
```

### Database Integration
Samuel uses AWS Lambda functions to securely connect to MongoDB, providing:
- Secure chat history storage
- Session data management
- Real-time data retrieval
- Scalable database operations


## Dynamic Configuration

The system now supports dynamic configuration through MongoDB. Each organization can have its own configuration for:

- Agent name and behavior
- Accepted file types
- RAG settings
- Context weights
- Analysis weights
- Sentiment weights
- Emotion weights
- LLM model selection

The configuration is automatically loaded for each request based on the [[organization_id]] and agent_name (defined in `settings.py`).
## API Endpoints

### Authentication
All endpoints require a Bearer token in the Authorization header.

### Session Management
- `GET /session` - Generate a new session ID for tracking conversations

### Chat Endpoints
- `GET /input` - Send a text message to the agent
  - Parameters:
    - `organization_id`: Your organization ID
    - `session_id`: Session ID from `/session` endpoint
    - `user_id`: User identifier
    - `message`: Your message to the agent
    - `Authorization`: Bearer token

- `POST /upload` - Upload a file for processing
  - Parameters:
    - `organization_id`: Your organization ID
    - `session_id`: Session ID from `/session` endpoint
    - `user_id`: User identifier
    - `message`: Context or question about the file
    - `file`: File to process (PDF, DOCX, TXT, CSV, XLSX)
    - `Authorization`: Bearer token

### Audio Processing
- `POST /audio` - Process audio files
  - Parameters:
    - `organization_id`: Your organization ID
    - `session_id`: Session ID from `/session` endpoint
    - `user_id`: User identifier
    - `prompt`: Context or question about the audio
    - `file`: Audio file to transcribe and process
    - `Authorization`: Bearer token

### Graph Generation
- `GET /get_graphs` - Generate graphs from data
  - Parameters:
    - `x`: Comma-separated x-axis values
    - `y`: Comma-separated y-axis values

### Recommendations
- `GET /get_chat_recommendations` - Get chat recommendations based on history
  - Parameters:
    - `organization_id`: Your organization ID
    - `user_id`: User identifier
    - `session_id`: Session ID from `/session` endpoint
    - `Authorization`: Bearer token

## Response Format

All endpoints return JSON responses with the following structure:
```json
{
    "message": "Response content",
    "response_time": "Time taken to generate response",
    "context_time": "Time taken to fetch context",
    "chat_history_time": "Time taken to fetch chat history",
    "insert_history_time": "Time taken to insert into history",
    "transcription_time": "Time taken to transcribe audio (for audio endpoints)"
}
```
## Example Usage

1. Start a new session:
```bash
curl -H "Authorization: Bearer your_token" http://localhost:8000/session
```

2. Send a message:
```bash
curl -H "Authorization: Bearer your_token" "http://localhost:8000/input?organization_id=org123&session_id=session456&user_id=user789&message=Hello%20SAMUEL"
```

3. Upload a file:
```bash
curl -X POST "http://localhost:8000/upload" \
  -H "Authorization: Bearer your_token" \
  -H "Content-Type: multipart/form-data" \
  -F "organization_id=org123" \
  -F "session_id=session456" \
  -F "user_id=user789" \
  -F "message=Please analyze this document" \
  -F "file=@document.pdf"
```

4. Process audio:
```bash
curl -X POST "http://localhost:8000/audio" \
  -H "Authorization: Bearer your_token" \
  -H "Content-Type: multipart/form-data" \
  -F "organization_id=org123" \
  -F "session_id=session456" \
  -F "user_id=user789" \
  -F "prompt=Please analyze this audio" \
  -F "file=@audio.mp3"
```