# Other services and terms

## SQS
### Backlog per instance
To calculate your backlog per instance, start with the ApproximateNumberOfMessages queue attribute to determine the length of the SQS queue (number of messages available for retrieval from the queue). Divide that number by the fleet's running capacity, which for an Auto Scaling group is the number of instances in the InService state, to get the backlog per instance.

### Acceptable backlog per instance
To calculate your target value, first determine what your application can accept in terms of latency. Then, take the acceptable latency value and divide it by the average time that an EC2 instance takes to process a message.

## Docker
### Docker swarm
A Docker swarm is a container orchestration tool, meaning that it allows the user to manage multiple containers deployed across multiple host machines. A swarm consists of multiple Docker hosts which run in swarm mode and act as managers (to manage membership and delegation) and workers (which run swarm services).

## ECS
### ECS service scheduler
Amazon ECS provides a service scheduler (for long-running tasks and applications), the ability to run tasks manually (for batch jobs or single run tasks), with Amazon ECS placing tasks on your cluster for you. You can specify task placement strategies and constraints that allow you to run tasks in the configuration you choose, such as spread out across Availability Zones. It is also possible to integrate with custom or third-party schedulers.

### ECS step scaling policy
Although Amazon ECS Service Auto Scaling supports using Application Auto Scaling step scaling policies, AWS recommends using target tracking scaling policies instead. For example, if you want to scale your service when CPU utilization falls below or rises above a certain level, create a target tracking scaling policy based on the CPU utilization metric provided by Amazon ECS.

With step scaling policies, you create and manage the CloudWatch alarms that trigger the scaling process. If the target tracking alarms don't work for your use case, you can use step scaling. You can also use target tracking scaling with step scaling for an advanced scaling policy configuration. For example, you can configure a more aggressive response when utilization reaches a certain level.

Step Scaling scales your cluster on various lengths of steps based on different ranges of thresholds. Target tracking on the other hand intelligently picks the smart lengths needed for the given configuration.

## Security

### Secrets Manager
AWS Secrets Manager enables you to easily rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle. Users and applications retrieve secrets with a call to Secrets Manager APIs, eliminating the need to hardcode sensitive information in plain text. Secrets Manager offers secret rotation with built-in integration for Amazon RDS, Amazon Redshift, and Amazon DocumentDB.

### AWS Private Certificate Authority
An AWS Private CA hierarchy provides strong security and restrictive access controls for the most-trusted root CA at the top of the trust chain, while allowing more permissive access and bulk certificate issuance for subordinate CAs lower on the chain.

With AWS Private CA, you can create private certificates to identify resources and protect data. You can create versatile certificate and CA configurations to identify and protect your resources, including servers, applications, users, devices, and containers.

The service offers direct integration with AWS IAM, and you can control access to AWS Private CA with IAM policies.

### SSM Parameter Store
AWS Systems Manager Parameter Store provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, and license codes as parameter values. SSM Parameter Store cannot be used to automatically rotate the database credentials.

### Systems Manager
AWS Systems Manager gives you visibility and control of your infrastructure on AWS. Systems Manager provides a unified user interface so you can view operational data from multiple AWS services and allows you to automate operational tasks across your AWS resources. Systems Manager cannot be used to store your secrets securely and automatically rotate the database credentials.

### Security Token Service
AWS provides AWS Security Token Service (AWS STS) as a web service that enables you to request temporary, limited-privilege credentials for users. This guide describes the AWS STS API.

By default, AWS Security Token Service (AWS STS) is available as a global service, and all AWS STS requests go to a single endpoint at https://sts.amazonaws.com

AWS STS supports AWS CloudTrail, a service that records AWS calls for your AWS account and delivers log files to an Amazon S3 bucket. By using information collected by CloudTrail, you can determine the requests successfully sent to AWS STS, as well as who sent the request, and when it was sent


### WAF
AWS WAF is a Web Application Firewall that lets you monitor the HTTP(S) requests that are forwarded to your protected web application resources. You can protect the following resource types:
- Amazon CloudFront distribution
- Amazon API Gateway REST API
- Application Load Balancer
- AWS AppSync GraphQL API
- Amazon Cognito user pool
- AWS App Runner service
- AWS Verified Access instance

AWS WAF lets you control access to your content. Based on criteria that you specify, such as the IP addresses that requests originate from or the values of query strings, the service associated with your protected resource responds to requests either with the requested content, with an HTTP 403 status code (Forbidden), or with a custom response.


### AWS Shield
AWS Shield is a managed DDoS protection service that safeguards applications running on AWS.


## Deployment
### CodeDeploy
- **In-place**: The application on each instance in the deployment group is stopped, the latest application revision is installed, and the new version of the application is started and validated.
- Blue/green

### EC2
- All at once
- Rolling
- Immutable
- Traffic splitting	
- **Blue/green**: The instances in a deployment group (the original environment) are replaced by a different set of instances

### Lambda
- **Blue/green**: Traffic is shifted in increments according to a canary, linear, or all-at-once deployment configuration.

### Beanstalk
- All at once
- Rolling
- Rolling with additional batch
- Immutable
- Traffic splitting

### CloudFormation
- Blue/green: Traffic is shifted from your current resources to your updated resources as part of an AWS CloudFormation stack update.