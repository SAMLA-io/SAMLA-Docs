We use MongoDB as our main database to back all of our infrastructure. Mainly, we store client and business information via our MongoDB database, and systems such as [[Samuel]] and [[Emile]] make us of it. 

In SAMLA, each company is assigned a database with their [[organization_id]] as the name, which will host all of their information within different collections. The collection names vary, but there are some standards that are used by our agents to facilitate information retrieval:

- chat_history : Used by [[Samuel]] and [[Emile]] to store data per user and [[session_id]] for every conversation made between user and agent.
- transcripts: Stores transcripts made by [[Emile]], along with their transcript name and other important metadata, which tends to be used by our frontend to provide information to our users.

We use the following clusters to store information:
- [[Cluster0]]: AWS / N. Virginia (us-east-1)
