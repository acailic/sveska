---
title: AWS CDA Practise test 3
layout: post
tags: [aws, cda, test]
date: 2020-08-17
---

## Security
- You can authenticate to your DB instance using AWS Identity and Access Management (IAM) database authentication. With this authentication method, you don't need to use a password when you connect to a DB instance. Instead, you use an authentication token. An authentication token is a unique string of characters that Amazon RDS generates on request. Each token has a lifetime of 15 minutes. You don't need to store user credentials in the database, because authentication is managed externally using IAM.
RDS MySQL - IAM database authentication works with MySQL and PostgreSQL.
RDS PostGreSQL - IAM database authentication works with MySQL and PostgreSQL.
- Generate a public SSH key from a private SSH key. Then, import the key into each of your AWS Regions
Here is the correct way of reusing SSH keys in your AWS Regions:
Generate a public SSH key (.pub) file from the private SSH key (.pem) file.
Set the AWS Region you wish to import to.
Import the public SSH key into the new Region.
- Use Envelope Encryption and reference the data as file within the code. While AWS KMS does support sending data up to 4 KB to be encrypted directly, envelope encryption can offer significant performance benefits. When you encrypt data directly with AWS KMS it must be transferred over the network. Envelope encryption reduces the network load since only the request and delivery of the much smaller data key go over the network. The data key is used locally in your application or encrypting AWS service, avoiding the need to send the entire block of data to AWS KMS and suffer network latency. AWS Lambda environment variables can have a maximum size of 4 KB. Additionally, the direct 'Encrypt' API of KMS also has an upper limit of 4 KB for the data payload. To encrypt 1 MB, you need to use the Encryption SDK and pack the encrypted file with the lambda function.
- Amazon API Gateway is an AWS service for creating, publishing, maintaining, monitoring, and securing REST, HTTP, and WebSocket APIs at any scale. API developers can create APIs that access AWS or other web services, as well as data stored in the AWS Cloud. AWS Security Token Service (STS) - AWS Security Token Service (AWS STS) is a web service that enables you to request temporary, limited-privilege credentials for AWS Identity and Access Management (IAM) users or for users that you authenticate (federated users). However, it is not supported by API Gateway. 
## Refactoring
- A Spot Instance is an unused EC2 instance that is available for less than the On-Demand price. Your Spot Instance runs whenever capacity is available and the maximum price per hour for your request exceeds the Spot price. Any instance present with unused capacity will be allocated.
You can specify that Amazon EC2 should do one of the following when it interrupts a Spot Instance:
Stop the Spot Instance
Hibernate the Spot Instance
Terminate the Spot Instance
The default is to terminate Spot Instances when they are interrupted.
-  Configure Application Auto Scaling to manage Lambda provisioned concurrency on a schedule.
Concurrency is the number of requests that a Lambda function is serving at any given time. If a Lambda function is invoked again while a request is still being processed, another instance is allocated, which increases the function's concurrency.Due to a surge in traffic, when Lambda functions scale, this causes the portion of requests that are served by new instances to have higher latency than the rest. To enable your function to scale without fluctuations in latency, use provisioned concurrency. By allocating provisioned concurrency before an increase in invocations, you can ensure that all requests are served by initialized instances with very low latency.
You can configure Application Auto Scaling to manage provisioned concurrency on a schedule or based on utilization. Use scheduled scaling to increase provisioned concurrency in anticipation of peak traffic. To increase provisioned concurrency automatically as needed, use the Application Auto Scaling API to register a target and create a scaling policy.
- Configure the data producer to retry with an exponential backoff.Increase the number of shards within your data streams to provide enough capacity. Amazon Kinesis Data Streams enables you to build custom applications that process or analyze streaming data for specialized needs. You can continuously add various types of data such as clickstreams, application logs, and social media to an Amazon Kinesis data stream from hundreds of thousands of sources. The capacity limits of an Amazon Kinesis data stream are defined by the number of shards within the data stream. The limits can be exceeded by either data throughput or the number of PUT records. While the capacity limits are exceeded, the put data call will be rejected with a ProvisionedThroughputExceeded exception. If this is due to a temporary rise of the data stream’s input data rate, retry (with exponential backoff) by the data producer will eventually lead to the completion of the requests. If this is due to a sustained rise of the data stream’s input data rate, you should increase the number of shards within your data stream to provide enough capacity for the put data calls to consistently succeed.
- "Bundle the dependencies in the source code during the last stage of CodeBuild".AWS CodeBuild is a fully managed build service. There are no servers to provision and scale, or software to install, configure, and operate.A typical application build process includes phases like preparing the environment, updating the configuration, downloading dependencies, running unit tests, and finally, packaging the built artifact. Downloading dependencies is a critical phase in the build process. These dependent files can range in size from a few KBs to multiple MBs. Because most of the dependent files do not change frequently between builds, you can noticeably reduce your build time by caching dependencies. This will allow the code bundle to be deployed to Elastic Beanstalk to have both the dependencies and the code, hence speeding up the deployment time to Elastic Beanstalk
## Monitoring
- Use the AWS CLI --dry-run option: The --dry-run option checks whether you have the required permissions for the action, without actually making the request, and provides an error response. If you have the required permissions, the error response is DryRunOperation, otherwise, it is UnauthorizedOperation.
- AWS CloudFormation gives developers and businesses an easy way to create a collection of related AWS and third-party resources and provision them in an orderly and predictable fashion. Parameter types enable CloudFormation to validate inputs earlier in the stack creation process. CloudFormation currently supports the following parameter types:
```
String – A literal string
Number – An integer or float
List<Number> – An array of integers or floats
CommaDelimitedList – An array of literal strings that are separated by commas
AWS::EC2::KeyPair::KeyName – An Amazon EC2 key pair name
AWS::EC2::SecurityGroup::Id – A security group ID
AWS::EC2::Subnet::Id – A subnet ID
AWS::EC2::VPC::Id – A VPC ID
List<AWS::EC2::VPC::Id> – An array of VPC IDs
List<AWS::EC2::SecurityGroup::Id> – An array of security group IDs
List<AWS::EC2::Subnet::Id> – An array of subnet IDs
```
- The network ACLs associated with the subnet must have rules to allow inbound and outbound traffic - The network access control lists (ACLs) that are associated with the subnet must have rules to allow inbound and outbound traffic on port 80 (for HTTP traffic) and port 443 (for HTTPs traffic). This is a necessary condition for Internet Gateway connectivity. The route table in the instance’s subnet should have a route to an Internet Gateway - A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed. The route table in the instance’s subnet should have a route defined to the Internet Gateway.
- You configure monitoring for EC2 instances using a launch configuration or template. Monitoring is enabled whenever an instance is launched, either basic monitoring (5-minute granularity) or detailed monitoring (1-minute granularity). AWS Management Console might have been used to create the launch configuration - By default, basic monitoring is enabled when you create a launch template or when you use the AWS Management Console to create a launch configuration. This could be the reason behind only the basic monitoring taking place.
## Development
- 200 GiB size volume with 15000 IOPS - This is an incorrect configuration. The maximum ratio of provisioned IOPS to requested volume size (in GiB) is 50:1. So, for a 200 GiB volume size, max IOPS possible is 20*50 = 10000 IOPS. 
- One read capacity unit represents one strongly consistent read per second for an item up to 4 KB in size. If you need to read an item that is larger than 4 KB, DynamoDB will need to consume additional read capacity units. 1) Item Size / 4KB, rounding to the nearest whole number. So, in the above case, 6KB / 4 KB = 1.5 or 2 read capacity units.
2) 1 read capacity unit per item (since strongly consistent read) × No of reads per second.So, in the above case, 2 x 10 = 20 read capacity units
- When you purchase a Reserved Instance for a specific Availability Zone, it's referred to as a Zonal Reserved Instance. Zonal Reserved Instances provide capacity reservations as well as discounts. Zonal Reserved Instances - A zonal Reserved Instance provides a capacity reservation in the specified Availability Zone. Capacity Reservations enable you to reserve capacity for your Amazon EC2 instances in a specific Availability Zone for any duration. This gives you the ability to create and manage Capacity Reservations independently from the billing discounts offered by Savings Plans or regional Reserved Instances
- Enable S3 and CloudWatch Logs integration - AWS CodeBuild monitors functions on your behalf and reports metrics through Amazon CloudWatch. These metrics include the number of total builds, failed builds, successful builds, and the duration of builds. You can monitor your builds at two levels: Project level, AWS account level. You can export log data from your log groups to an Amazon S3 bucket and use this data in custom processing and analysis, or to load onto other systems.
- Use ConsistentRead = true while doing GetItem operation for any item.DynamoDB supports eventually consistent and strongly consistent reads. Eventually Consistent Reads. When you read data from a DynamoDB table, the response might not reflect the results of a recently completed write operation. The response might include some stale data. If you repeat your read request after a short time, the response should return the latest data. Strongly Consistent Reads. When you request a strongly consistent read, DynamoDB returns a response with the most up-to-date data, reflecting the updates from all prior write operations that were successful. DynamoDB uses eventually consistent reads by default. Read operations (such as GetItem, Query, and Scan) provide a ConsistentRead parameter. If you set this parameter to true, DynamoDB uses strongly consistent reads during the operation. As per the given use-case, to make sure that only the last updated value of any item is used in the application, you should use strongly consistent reads by setting ConsistentRead = true for GetItem operation.
- Amazon Kinesis Data Firehose is a fully managed service for delivering real-time streaming data to destinations such as Amazon Simple Storage Service (Amazon S3), Amazon Redshift, Amazon Elasticsearch Service (Amazon ES), and Splunk. With Kinesis Data Firehose, you don't need to write applications or manage resources. You configure your data producers to send data to Kinesis Data Firehose, and it automatically delivers the data to the destination that you specified. Amazon ElastiCache with Amazon S3 as backup - Amazon ElastiCache is a fully managed in-memory data store, compatible with Redis or Memcached. ElastiCache is NOT a supported destination for Amazon Kinesis Data Firehose.
- EBS volumes are AZ locked.An Amazon EBS volume is a durable, block-level storage device that you can attach to your instances. After you attach a volume to an instance, you can use it as you would use a physical hard drive. EBS volumes are flexible. For current-generation volumes attached to current-generation instance types, you can dynamically increase size, modify the provisioned IOPS capacity, and change volume type on live production volumes.When you create an EBS volume, it is automatically replicated within its Availability Zone to prevent data loss due to the failure of any single hardware component. You can attach an EBS volume to an EC2 instance in the same Availability Zone.
- The performance of gp2 volumes is tied to volume size, which determines the baseline performance level of the volume and how quickly it accumulates I/O credits; larger volumes have higher baseline performance levels and accumulate I/O credits faster. 5.3 TiB - General Purpose SSD (gp2) volumes offer cost-effective storage that is ideal for a broad range of workloads. These volumes deliver single-digit millisecond latencies and the ability to burst to 3,000 IOPS for extended periods of time. Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size.
- Use the DynamoDB transactional read and write APIs on the table items as a single, all-or-nothing operation
You can use DynamoDB transactions to make coordinated all-or-nothing changes to multiple items both within and across tables. Transactions provide atomicity, consistency, isolation, and durability (ACID) in DynamoDB, helping you to maintain data correctness in your applications. Complete both operations on RDS MySQL in a single transaction block
Amazon Relational Database Service (Amazon RDS) makes it easy to set up, operate, and scale a relational database with support for transactions in the cloud. A relational database is a collection of data items with pre-defined relationships between them. RDS supports the most demanding database applications. You can choose between two SSD-backed storage options: one optimized for high-performance Online Transaction Processing (OLTP) applications, and the other for cost-effective general-purpose use.
- Amazon EC2 Auto Scaling is a fully managed service designed to launch or terminate Amazon EC2 instances automatically to help ensure you have the correct number of Amazon EC2 instances available to handle the load for your application.Amazon EC2 Auto Scaling cannot add a volume to an existing instance if the existing volume is approaching capacity - A volume is attached to a new instance when it is added. Amazon EC2 Auto Scaling doesn't automatically add a volume when the existing one is approaching capacity. You can use the EC2 API to add a volume to an existing instance.Amazon EC2 Auto Scaling works with both Application Load Balancers and Network Load Balancers - Amazon EC2 Auto Scaling works with Application Load Balancers and Network Load Balancers including their health check feature. 
- Use delay queues to postpone the delivery of new messages to the queue for a few seconds. Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications. SQS offers two types of message queues. Standard queues offer maximum throughput, best-effort ordering, and at-least-once delivery. SQS FIFO queues are designed to guarantee that messages are processed exactly once, in the exact order that they are sent. Delay queues let you postpone the delivery of new messages to a queue for several seconds, for example, when your consumer application needs additional time to process messages. If you create a delay queue, any messages that you send to the queue remain invisible to consumers for the duration of the delay period. The default (minimum) delay for a queue is 0 seconds. The maximum is 15 minutes.
- AWS CloudFormation provides several built-in functions that help you manage your stacks. Intrinsic functions are used in templates to assign values to properties that are not available until runtime. !GetAtt - The Fn::GetAtt intrinsic function returns the value of an attribute from a resource in the template. This example snippet returns a string containing the DNS name of the load balancer with the logical name myELB - YML : !GetAtt myELB.DNSName JSON : "Fn::GetAtt" : [ "myELB" , "DNSName" ]
 
## Deployment
- Define an appspec.yml file in the root directory: An AppSpec file must be a YAML-formatted file named appspec.yml and it must be placed in the root of the directory structure of an application's source code.The AppSpec file is used to:Map the source files in your application revision to their destinations on the instance.
Specify custom permissions for deployed files.
Specify scripts to be run on each instance at various stages of the deployment process.
During deployment, the CodeDeploy agent looks up the name of the current event in the hooks section of the AppSpec file. If the event is not found, the CodeDeploy agent moves on to the next step. If the event is found, the CodeDeploy agent retrieves the list of scripts to execute. The scripts are run sequentially, in the order in which they appear in the file. The status of each script is logged in the CodeDeploy agent log file on the instance.
If a script runs successfully, it returns an exit code of 0 (zero). If the CodeDeploy agent installed on the operating system doesn't match what's listed in the AppSpec file, the deployment fails.
- Application Load Balancer + ECS: Amazon Elastic Container Service (Amazon ECS) is a highly scalable, fast, container management service that makes it easy to run, stop, and manage Docker containers on a cluster. You can host your cluster on a serverless infrastructure that is managed by Amazon ECS by launching your services or tasks using the Fargate launch type. For more control over your infrastructure, you can host your tasks on a cluster of Amazon Elastic Compute Cloud (Amazon EC2) instances that you manage by using the EC2 launch type. An Application load balancer distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones. A listener checks for connection requests from clients, using the protocol and port that you configure. The rules that you define for a listener determine how the load balancer routes requests to its registered targets. Each rule consists of a priority, one or more actions, and one or more conditions.
- Deploy the new application version using 'Immutable' deployment policy. With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without having to learn about the infrastructure that runs those applications. Elastic Beanstalk reduces management complexity without restricting choice or control. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring. The 'Immutable' deployment policy ensures that your new application version is always deployed to new instances, instead of updating existing instances. It also has the additional advantage of a quick and safe rollback in case the deployment fails. In an immutable update, a second Auto Scaling group is launched in your environment and the new version serves traffic alongside the old version until the new instances pass health checks. In case of deployment failure, the new instances are terminated, so the impact is minimal.
- 