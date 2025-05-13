We use AWS Lamba to allow for serverless functions to run on the cloud, at a very cheap cost. These functions execute very little code, and serve only to streamline our internal processes and data workflow. 

AWS Lambda requires a layer if any external packages are needed. These layers can easily be generated, though external help will be needed (see web information). Currently, there are two layers: 

- `aws_pymongo_layer` contains the required packages to run [[MongoDB]] related functions
- `aws_cognito_layer` contains the required packages to connect with AWS Cognito

We use Python 3.12 as our main programming language for AWS Lambda, and we currently have 3 main functions to interface with our [[MongoDB]] database:  

The main reason for using AWS Lambda is for creating a common interface with our MongoDB clusters. The following functions are connected to the same cluster ([[Cluster0]]), and are used to upload and retrieve data to a specific database and collection:
- [[get_one]]: Retrieves a single document from MongoDB based on a query
- [[get_all]]: Fetches all documents from a specified MongoDB collection
- [[get_many]]: Retrieves multiple documents from MongoDB using a custom query
- [[insert_one]]: Inserts a single document into a MongoDB collection
- [[insert_many]]: Bulk inserts multiple documents into a MongoDB collection

The code for these functions can be found [here](https://github.com/SAMLA-io/mongo-api)

Using these functions as a base, there are some derived functions that call these main functions to provide more specific results without the need of doing much queries.  
- [[get_all_conversations]]
## Graphic overview

![[MongoDB AWS.drawio.png]]

