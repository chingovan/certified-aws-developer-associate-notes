# ECS
Notes
- Cross-AZ
- An ECS Task is a running Docker Container
- An AWS ECS cluster is a logical grouping of tasks or services
- Docker images can be stored in ASW ECR
- ECS services are used to maintain a desired count of tasks
- ECS container instance is EC2 instance + ECS agent running on it.
- We can run multi-container inside an ECS instance and can scale
- Serverless with AWS Fargat - managed for you and fully scalable

## Components
- Cluster: Logical grouping of tasks or services
- Container instance: EC2 instance running ECS agent
- Task definition: Blueprint that describes how a docker container should launch
- Task: A running container using settings in a Task Definition
- Service: Defines long running tasks - can control task count with Auto Scaling and attach an ELS

## Launch Types
- EC2
  - You explicitly provision EC2 instances
  - You are responsible for managing EC2 instances
  - Charged per running EC2 instances
  - EFS and EBS integration
  - You handle cluster optimization
  - More granular control over infarstructure
- Farget
  - Farget automatically provisions resources 
  - Farget provisions and manages compute
  - Charged for running tasks
  - No EBS integration
  - Farget handles cluster optimization
  - Limited control, infarstructure is automated

## IAM Roles
- EC2 launch type
  - The container instance IAM role provides permission to the host
  - The ECS taks IAM role provides permission to the container
- Fargate
    - There is only IAM task roles

## Task placement strategies
Task plancement is applied for EC2 launch type only
- **binpack**: Place tasks based on the least available amount of CPU or memory. This minimizes the number of instances in use.
- **random**: Place tasks randomly.
- **spread**: Place tasks evenly based on the specified value.
  - Accepted values are instanceId (or host, which has the same effect), or any platform or custom attribute that is applied to a container instance, such as attribute:ecs.availability-zone.
  - Service tasks are spread based on the tasks from that service. 
  - Standalone tasks are spread based on the tasks from the same task group.

## Auto Scaling
There are 2 types
- Service auto scaling: Automatically adjusts the desired task count up or down using the Application Auto Scaling service
  - Target tracking scaling policies - Increase or decrease the number of tasks that your services runs based on a target value for a specific CloudWath metrics
  - Step scaling polices - Increase or decrease the number of tasks that your service runs in responses to CloudWatch alarms. Step scaling is based on a set of scaling adjustments, knows as step adjustments, which vary based on the size of alarm breach
  - Scheduled scaling - Increase or descrease the number of tasks that your service runs based on the date and time
- Cluster auto scaling: uses a capacity provider to scale the number of EC2 cluster instances using EC2 Auto Scaling