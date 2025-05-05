> The session id refers to the ID of the currently ongoing session with a specific Agent or system. The **front-end** should retrieve this id, and pass it on all API calls. It helps us keep a record on what and when information was exchanged between different systems. For example, using a specific session_id, [[Samuel]] can retrieve an entire chat history thanks to the ID stored per prompt request 

## How is it generated? 

Although each system and agents allow you to generate a session_id (which should be done before performing any important calls i.e when starting a conversation with [[Samuel]], [[Emile]] or [[Sarah]]), they all work the same way, with the same code: 

```python
import uuid

def generate_session_id():
    return str(uuid.uuid4())
    
```

For context, a UUID is a 32-long number that is effectively unique. 

> A Universally Unique Identifier (UUID) is a 128-bit label used to uniquely identify objects in computer systems \- Wikipedia (2025)

