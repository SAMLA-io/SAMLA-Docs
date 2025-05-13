Container applications are deployed and managed using Amazon Elastic Container Service. This helps us orchestrate and run our containerized applications at scale, with built-in support for load balancing and auto-scaling.

All Agents are deployed as containerized applications running on ECS. We tend to use Fargate to run the containers, as it is a more cost-effective solution than EC2. Regarding specs, we use the .25 vCPU | .5 GB RAM configuration, as it is more than enough for our purposes, at least for now.

## Task Definition Script

To facilitate the creation of ECS task definitions, we use the `define_task.sh` script. This interactive script helps create task definitions with the following features:

- Supports both Fargate and EC2 launch types
- Allows selection of existing ECR repositories and image tags
- Configures container ports, CPU, and memory specifications
- Sets up CloudWatch logging automatically
- Creates task definitions with proper IAM roles

The script can be found in our agent configuration repository and is used to standardize the creation of task definitions across different environments.

- [`define_task.sh`](https://github.com/SAMLA-io/agent-config/blob/main/define_task.sh): Interactive script for creating ECS task definitions

Note: The script is designed to be used in a CI/CD pipeline, but can also be used manually. No CI/CD pipeline exists yet, so it is recommended to use the script manually. Also, the script just creates the task definition, it does not deploy the service.