---
title: AWS CDA Practise test 5
layout: post
tags: [aws, cda, test]
date: 2020-08-17
---
### Monitoring
- Your company manages hundreds of EC2 instances running on Linux OS. The instances are configured in several Availability Zones in the eu-west-3 region. Your manager has requested to collect system memory metrics on all EC2 instances using a script.
Which of the following solutions will help you collect this data?:Use a cron job on the instances that pushes the EC2 RAM statistics as a Custom metric into CloudWatch. The Amazon CloudWatch Monitoring Scripts for Amazon Elastic Compute Cloud (Amazon EC2) Linux-based instances demonstrate how to produce and consume Amazon CloudWatch custom metrics. These Perl scripts comprise a fully functional example that reports memory, swap, and disk space utilization metrics for a Linux instance. You can set a cron schedule for metrics reported to CloudWatch and report memory utilization to CloudWatch every x minutes.
- You are revising options that would be best for monitoring a few EC2 instances you currently manage. Amazon CloudWatch has metrics available to monitor your EC2 instances for CPU load, I/O, and network I/O. Your budget does not allow for spending on monitoring so using the default monitoring available is your preferred choice.
With default monitoring, at what interval will these metrics be collected?:5 minutes.By default, your instance is enabled for basic monitoring and Amazon EC2 sends metric data to CloudWatch in 5-minute periods. You can optionally enable detailed monitoring. After you enable detailed monitoring, the Amazon EC2 console displays monitoring graphs with a 1-minute period for the instance.
The following describes the data interval and charge for basic and detailed monitoring for instances. Basic monitoring Data is available automatically in 5-minute periods at no charge. Detailed monitoring Data is available in 1-minute periods for an additional charge.
- An organization uses Alexa as its intelligent assistant to improve productivity throughout the organization. A group of developers manages custom Alexa Skills written in Node.Js to control conference-room equipment settings and start meetings using voice activation. The manager has requested developers that all functions code should be monitored for error rates with the possibility of creating alarms on top of them.
Which of the following options should be chosen? (select two):CloudWatch Alarms.CloudWatch Metrics.
- A development team has inherited a web application running in the us-east-1 region with three availability zones (us-east-1a, us-east1-b, and us-east-1c) whose incoming web traffic is routed by a load balancer. When one of the EC2 instances hosting the web application crashes, the team realizes that the load balancer continues to route traffic to that instance causing intermittent issues.
Which of the following should the development team do to minimize this problem?: Enable Health Checks. To discover the availability of your EC2 instances, a load balancer periodically sends pings, attempts connections, or sends requests to test the EC2 instances. 
### Security
- An IT company has a web application running on Amazon EC2 instances that needs read-only access to an Amazon DynamoDB table.
As a Developer Associate, what is the best-practice solution you would recommend to accomplish this task?:Create an IAM role with an AmazonDynamoDBReadOnlyAccess policy and apply it to the EC2 instance profile. Instead, create an IAM role that you attach to the EC2 instance to give temporary security credentials to applications running on the instance. When an application uses these credentials in AWS, it can perform all of the operations that are allowed by the policies attached to the role.
So for the given use-case, you should create an IAM role with an AmazonDynamoDBReadOnlyAccess policy and apply it to the EC2 instance profile.
- A cybersecurity company is publishing critical log data to a log group in Amazon CloudWatch Logs, which was created 3 months ago. The company must encrypt the log data using an AWS KMS customer master key (CMK), so any future data can be encrypted to meet the company’s security guidelines.
How can the company address this use-case?: Use the AWS CLI associate-kms-key  command and specify the KMS key ARN. 
- You have a web application hosted on EC2 that makes GET and PUT requests for objects stored in Amazon Simple Storage Service (S3) using the SDK for PHP. As the security team completed the final review of your application for vulnerabilities, they noticed that your application uses hardcoded IAM access key and secret access key to gain access to AWS services. They recommend you leverage a more secure setup, which should use temporary credentials if possible.
Which of the following options can be used to address the given use-case? Use an IAM Instance Role.
- Your company leverages Amazon CloudFront to provide content via the internet to customers with low latency. Aside from latency, security is another concern and you are looking for help in enforcing end-to-end connections using HTTPS so that content is protected.
Which of the following options is available for HTTPS in AWS CloudFront?:Between clients and CloudFront as well as between CloudFront and backend.
- You are a manager for a tech company that has just hired a team of developers to work on the company's AWS infrastructure. All the developers are reporting to you that when using the AWS CLI to execute commands it fails with the following exception: You are not authorized to perform this operation. Encoded authorization failure message: 6h34GtpmGjJJUm946eDVBfzWQJk6z5GePbbGDs9Z2T8xZj9EZtEduSnTbmrR7pMqpJrVYJCew2m8YBZQf4HRWEtrpncANrZMsnzk.
Which of the following actions will help developers decode the message?:AWS STS decode-authorization-message
- A media company is building an application that needs to store video files in Amazon S3. Management requires that the files be encrypted before they are sent to Amazon S3 for storage. The encryption keys need to be managed by an in-house security team but the key itself is stored on AWS.
Which solution should the company use to meet these requirements?: Use client-side encryption with an AWS KMS managed customer master key (CMK).
- You have a popular web application that accesses data stored in an Amazon Simple Storage Service (S3) bucket. Developers use the SDK to maintain the application and add new features. Security compliance requests that all new objects uploaded to S3 be encrypted using SSE-S3 at the time of upload. Which of the following headers must the developers add to their request?:x-amz-server-side-encryption': 'AES256'
Server-side encryption protects data at rest. Amazon S3 encrypts each object with a unique key. As an additional safeguard, it encrypts the key itself with a master key that it rotates regularly. Amazon S3 server-side encryption uses one of the strongest block ciphers available to encrypt your data, 256-bit Advanced Encryption Standard (AES-256).
- An organization recently began using AWS CodeCommit for its source control service. A compliance security team visiting the organization was auditing the software development process and noticed developers making many git push commands within their development machines. The compliance team requires that encryption be used for this activity.
How can the organization ensure source code is encrypted in transit and at rest?:Repositories are automatically encrypted at rest.
- As part of internal regulations, you must ensure that all communications to Amazon S3 are encrypted. For which of the following encryption mechanisms will a request get rejected if the connection is not using HTTPS?:SSE-C. Server-side encryption is about protecting data at rest. Server-side encryption encrypts only the object data, not object metadata. Using server-side encryption with customer-provided encryption keys (SSE-C) allows you to set your encryption keys.
- Your company stores confidential data on an Amazon Simple Storage Service (S3) bucket. New security compliance guidelines require that files be stored with server-side encryption. The encryption used must be Advanced Encryption Standard (AES-256) and the company does not want to manage S3 encryption keys.
Which of the following options should you use?:SSE-S3. Using Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3), each object is encrypted with a unique key employing strong multi-factor encryption. As an additional safeguard, it encrypts the key itself with a master key that it regularly rotates. Amazon S3 server-side encryption uses one of the strongest block ciphers available, 256-bit Advanced Encryption Standard (AES-256), to encrypt your data.
- You are planning to build a fleet of EBS-optimized EC2 instances to handle the load of your new application. Due to security compliance, your organization wants any secret strings used in the application to be encrypted to prevent exposing values as clear text.
The solution requires that decryption events be audited and API calls to be simple. How can this be achieved? (select two):Audit using CloudTrail.Store the secret as SecureString in SSM Parameter Store
- An analytics company is using Kinesis Data Streams (KDS) to process automobile health-status data from the taxis managed by a taxi ride-hailing service. Multiple consumer applications are using the incoming data streams and the engineers have noticed a performance lag for the data delivery speed between producers and consumers of the data streams.
 As a Developer Associate, which of the following options would you suggest for improving the performance for the given use-case?:Use Enhanced Fanout feature of Kinesis Data Streams. Amazon Kinesis Data Streams (KDS) is a massively scalable and durable real-time data streaming service. KDS can continuously capture gigabytes of data per second from hundreds of thousands of sources such as website clickstreams, database event streams, financial transactions, social media feeds, IT logs, and location-tracking events.
### Refactoring
- A development team uses the AWS SDK for Java to maintain an application that stores data in AWS DynamoDB. The application makes use of Scan operations to return several items from a 25 GB table. There is no possibility of creating indexes to retrieve these items predictably. Developers are trying to get these specific rows from DynamoDB as fast as possible.
Which of the following options can be used to improve the performance of the Scan operation?:Use parallel scans. 
### Development with AWS
- You are assigned as the new project lead for a web application that processes orders for customers. You want to integrate event-driven processing anytime data is modified or deleted and use a serverless approach using AWS Lambda for processing stream events.
Which of the following databases should you choose from?:Kinesis is not a database. DynamoDB
- You have uploaded a zip file to AWS Lambda that contains code files written in Node.Js. When your function is executed you receive the following output, 'Error: Memory Size: 3008 MB Max Memory Used'.
 Which of the following explains the problem? Your Lambda function was deployed with 3008MB of RAM, but it seems your code requested or used more than that, so the Lambda function failed.
- A senior cloud engineer designs and deploys online fraud detection solutions for credit card companies processing millions of transactions daily. The Elastic Beanstalk application sends files to Amazon S3 and then sends a message to an Amazon SQS queue containing the path of the uploaded file in S3. A solution architect recommended that since PUTS of existing objects in S3 deliver eventual consistency and we want to minimize the risk of consumers reading old data, it would be preferable to introduce a per-message lag so that consumers won't find a message in SQS until it has been in the queue for at least 10 seconds.
 Which SQS feature should the developer leverage?:Delay queues let you postpone the delivery of new messages to a queue for several seconds, for example, when your consumer application needs additional time to process messages. 
- You are a system administrator whose company recently moved its production application to AWS and migrated data from MySQL to AWS DynamoDB. You are adding new tables to AWS DynamoDB and need to allow your application to query your data by the primary key and an alternate key. This option must be added when first creating tables otherwise changes cannot be made afterward.
 Which of the following actions should you take?:Create a LSI. Local secondary indexes are created at the same time that you create a table. You cannot add a local secondary index to an existing table, nor can you delete any local secondary indexes that currently exist.
- DevOps engineers are developing an order processing system where notifications are sent to a department whenever an order is placed for a product. The system also pushes identical notifications of the new order to a processing module that would allow EC2 instances to handle the fulfillment of the order. In the case of processing errors, the messages should be allowed to be re-processed at a later stage and never lost.
 Which of the following solutions can be used to address this use-case?SNS + SQS.Amazon SNS enables message filtering and fanout to a large number of subscribers, including serverless functions, queues, and distributed systems. Additionally, Amazon SNS fans out notifications to end users via mobile push messages, SMS, and email.
- You have a popular three-tier web application that is used by users throughout the globe receiving thousands of incoming requests daily. You have AWS Route 53 policies to automatically distribute weighted traffic to the API resources located at URL api.global.com.
 What is an alternative way of distributing traffic to a web application?:CloudFront - Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds.
- You have an Amazon Kinesis Data Stream with 10 shards, and from the metrics, you are well below the throughput utilization of 10 MB per second to send data. You send 3 MB per second of data and yet you are receiving ProvisionedThroughputExceededException errors frequently.
 What is the likely cause of this?:The partition key that you have selected isn't distributed enough
- Your application sends messages to an Amazon Simple Queue Service (SQS) queue frequently, which are then polled by another application that specifies which message to retrieve.
  Which of the following options describe the maximum number of messages that can be retrieved at one time?: 10. After you send messages to a queue, you can receive and delete them. When you request messages from a queue, you can't specify which messages to retrieve. Instead, you specify the maximum number of messages (up to 10) that you want to retrieve.
### Deployment
- Your company is in the process of building a DevOps culture and is moving all of its on-premise resources to the cloud using serverless architectures and automated deployments. You have created a CloudFormation template in YAML that uses an AWS Lambda function to pull HTML files from GitHub and place them into an Amazon Simple Storage Service (S3) bucket that you specify.     Which of the following AWS CLI commands can you use to upload AWS Lambda functions and AWS CloudFormation templates to AWS?:cloudformation package and cloudformation deploy.AWS CloudFormation gives developers and businesses an easy way to create a collection of related AWS and third-party resources and provision them in an orderly and predictable fashion.
- You have a Java-based application running on EC2 instances loaded with AWS CodeDeploy agents. You are considering different options for deployment, one is the flexibility that allows for incremental deployment of your new application versions and replaces existing versions in the EC2 instances. The other option is a strategy in which an Auto Scaling group is used to perform a deployment.
Which of the following options will allow you to deploy in this manner? (Select two):In-place Deployment
The application on each instance in the deployment group is stopped, the latest application revision is installed, and the new version of the application is started and validated. You can use a load balancer so that each instance is deregistered during its deployment and then restored to service after the deployment is complete.
Blue/green Deployment. With a blue/green deployment, you provision a new set of instances on which CodeDeploy installs the latest version of your application. CodeDeploy then re-routes load balancer traffic from an existing set of instances running the previous version of your application to the new set of instances running the latest version. After traffic is re-routed to the new instances, the existing instances can be terminated.
- An e-commerce company has implemented AWS CodeDeploy as part of its AWS cloud CI/CD strategy. The company has configured automatic rollbacks while deploying a new version of its flagship application to Amazon EC2.
What occurs if the deployment of the new version fails?:A new deployment of the last known working version of the application is deployed with a new deployment ID
AWS CodeDeploy is a service that automates code deployments to any instance, including Amazon EC2 instances and instances running on-premises. AWS CodeDeploy makes it easier for you to rapidly release new features, helps you avoid downtime during deployment, and handles the complexity of updating your applications.
- An IT company is using AWS CloudFormation to manage its IT infrastructure. It has created a template to provision a stack with a VPC and a subnet. The output value of this subnet has to be used in another stack.
As a Developer Associate, which of the following options would you suggest to provide this information to another stack?: Use 'Export' field in the Output section of the stack's template.To share information between stacks, export a stack's output values. Other stacks that are in the same AWS account and region can import the exported values.
To export a stack's output value, use the Export field in the Output section of the stack's template. To import those values, use the Fn::ImportValue function in the template for the other stacks.

- As a site reliability engineer, you are responsible for improving the company’s deployment by scaling and automating applications. As new application versions are ready for production you ensure that the application gets deployed to different sets of EC2 instances at different times allowing for a smooth transition.
Using AWS CodeDeploy, which of the following options will allow you to do this?: CodeDeploy Deployment Groups. You can specify one or more deployment groups for a CodeDeploy application. The deployment group contains settings and configurations used during the deployment. Most deployment group settings depend on the compute platform used by your application. Some settings, such as rollbacks, triggers, and alarms can be configured for deployment groups for any compute platform.
In an EC2/On-Premises deployment, a deployment group is a set of individual instances targeted for deployment. A deployment group contains individually tagged instances, Amazon EC2 instances in Amazon EC2 Auto Scaling groups, or both.