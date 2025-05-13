Container images are stored in Amazon Elastic Container Registry. This help us have a central place for storing images, instead of publishing them to Docker Hub for security reasons. 

All Agents are stored in a Docker container that is actively pushed to ECR. To facilitate pushing to ECR, a bash script has been developed that automatically pushes a Docker image to ECR in a single prompt.

- [`bp_agent.bash`](https://github.com/SAMLA-io/agent-config/blob/main/bp_agent.sh): Builds and pushes a Docker image to AWS ECR for the BP Agent