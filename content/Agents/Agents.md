SAMLA Agents are the main selling point for the organization. All Agents are version controlled and found in the [SAMLA Enterprise Tools](https://github.com/SAMLA-io/SAMLA-Enterprise-Tools.git) Github repository. 
## Agents list
- [[Samuel]]
- [[Emile]]
- [[Sarah]]

## Important notes
When interfacing with SAMLA Agents, two things are very important (depending on the system)
- [[organization_id]]
- [[session_id]]

All agents use [[AWS Lambda]] functions by default (and should do so at all times) to connect to the MongoDB database for storing and retrieving chat history and session data. This ensures secure, scalable, and reliable data management across all agent interactions.

## How to create an agent? 

1. Create a new folder in the [SAMLA Enterprise Tools](https://github.com/SAMLA-io/SAMLA-Enterprise-Tools.git) repository
2. You must follow the template provided in the [SAMLA Agent](https://github.com/SAMLA-io/SAMLA-Agent) repository
3. Set up the environment:
   - Create a `.env` file with required variables:
     ```
     OPENAI_API_KEY=your_openai_api_key
     RAG_URL=your_rag_service_url
     RAG_COLLECTION=your_rag_collection_name
     MONGO_AWS_URL=your_mongo_url
     MONGO_AWS_TOKEN=your_mongo_token
     MONGO_CHAT_HISTORY_COLLECTION=your_collection_name
     ```
4. Configure the agent in `setup.py`:
   - Initialize dotenv variables
   - Set up LLMs (GPT-4, GPT-4 Optimized, GPT-3.5 Turbo)
   - Configure the orchestrator with appropriate weights
   - Create the agent with desired file format support and RAG capabilities
5. Add the agent's code to the file
6. Add the agent's configuration to the `config.json` file
7. Add the agent's Dockerfile to the folder
8. Add the agent's README.md file to the folder
9. Add the agent's requirements.txt file to the folder

## Agent Features

Your agent will inherit these capabilities from the SAMLA Agent template:
- 🤖 Multi-model orchestration with GPT-4, GPT-4 Optimized, and GPT-3.5 Turbo
- 📚 RAG (Retrieval-Augmented Generation) support
- 📄 Multiple file format support (PDF, DOCX, TXT, CSV, XLSX)
- 🎤 Audio transcription support
- 📊 Graph generation capabilities
- 🔄 Intelligent model selection based on task requirements
- 💡 Sentiment and domain-aware processing
- 💬 Chat history and recommendations

## API Endpoints

Your agent will automatically include these endpoints, though you can add more if needed:
- `GET /session` - Generate a new session ID
- `GET /input` - Send text messages
- `POST /upload` - Upload files for processing
- `POST /audio` - Process audio files
- `GET /get_graphs` - Generate graphs from data
- `GET /get_chat_recommendations` - Get chat recommendations