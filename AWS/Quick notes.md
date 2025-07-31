# Services:
## Security

- **AWS Identity and Access Management (IAM):** Manage users, groups, roles, and permissions to securely control access to AWS resources.
- **Amazon GuardDuty:** Continuously monitors for malicious activity and unauthorized behavior using machine learning and threat intelligence.
- **AWS Key Management Service (KMS):** Create and control encryption keys used to encrypt your data across AWS services.
- **AWS Web Application Firewall (WAF):** Protect web applications by filtering and monitoring HTTP traffic based on customizable rules.
- **AWS Shield:** DDoS protection service, with Standard automatically enabled and Advanced offering expanded detection and mitigation
- **Amazon Cognito:** Handle user sign-up, sign-in, and access control for web and mobile apps with built-in authentication and authorization.

## Network

- **Amazon Virtual Private Cloud (VPC):** Provision isolated network environments and control IP address ranges, subnets, and route tables.
- **Elastic Load Balancing (ELB):** Distribute incoming application traffic across multiple targets to improve availability and fault tolerance.
- **AWS Direct Connect:** Establish a private, high-bandwidth network connection between your on-premises data center and AWS.
- **Amazon Route 53:** Highly available and scalable Domain Name System (DNS) web service for domain registration and routing.
- **AWS Transit Gateway:** Simplify complex networks by centrally connecting VPCs and on-premises networks through a single gate

## Compute

- **EC2**: Virtual machines with many sizes. Has `on-demand`, `spot` instance type
- **AWS Lambda**: Run code correspond to events. Serverless: Don't care about managing and provisioning servers
- **AWS Elastic Beanstalk:** Deploy and scale web applications and services automatically, handling capacity provisioning and load balancing.
- **Amazon Lightsail:** Simplified virtual private servers with predictable pricing for small-scale applications and quick deployments.
- **AWS Batch:** Efficiently run hundreds to thousands of batch computing jobs on AWS without managing infrastructure.
## Containers

- **Amazon Elastic Container Service (ECS):** Fully managed container orchestration service with deep AWS integration.
- **Amazon Elastic Kubernetes Service (EKS):** Run Kubernetes clusters on AWS without needing to install or operate your own control plane.
- **AWS Fargate:** Serverless compute engine for containers that works with both ECS and EKS, removing the need to manage servers.
- **AWS App Runner:** Deploy containerized web applications and APIs directly from source code or container image with automatic scaling.
## Storage

- **S3:** Object storage with virtually unlimited scalability, data availability, and security.
- **Amazon Glacier (S3 Glacier):** Low-cost archive storage with configurable retrieval times ranging from minutes to hours.
- **Amazon Elastic Block Store (EBS):** Persistent block-level storage volumes for use with EC2 instances.
- **Amazon Elastic File System (EFS):** Scalable, fully managed file storage for use with AWS compute services and on-premises resources.
- **AWS Storage Gateway:** Blend on-premises environments with cloud storage, offering file, volume, and tape gateways. Integrate data from on-prem to AWS. Data will be replicated to AWS
## Database managed service

- **Amazon Relational Database Service (RDS):** Managed relational database service supporting multiple engines like MySQL, PostgreSQL, and SQL Server. (Relational)
- **Amazon DynamoDB:** Fully managed NoSQL database offering single-digit millisecond performance at any scale. (NoSQL)
- **Amazon Aurora:** MySQL- and PostgreSQL-compatible relational database with up to five times the performance of standard MySQL.
- **Amazon Redshift:** Fast, fully managed data warehousing service for petabyte-scale analytics.
- **Amazon DocumentDB:** Managed document database service compatible with MongoDB workloads. (NoSQL)

## Deployment

- **AWS CloudFormation:** Model and provision AWS resources using templates to automate infrastructure as code.
- **AWS Cloud Development Kit (CDK):** Define cloud infrastructure using familiar programming languages for higher-level abstractions.
- **AWS OpsWorks:** Configuration management service that uses Chef and Puppet automation platforms for server configuration.
- **AWS Systems Manager:** Gain operational insights and automate tasks across AWS resources for secure and compliant management.
## Monitoring

- **Amazon CloudWatch:** Collect and track metrics, collect and monitor log files, and set alarms to react to changes in your AWS resources.
- **AWS X-Ray:** Analyze and debug distributed applications in production or under development to trace requests and visualize service maps.
- **AWS CloudTrail:** Record account activity and API calls for audit and compliance purposes.
- **Amazon EventBridge:** Serverless event bus that makes it easy to connect application data from your own apps, third-party SaaS, and AWS services.
- **AWS Config:** Continuously assess, audit, and evaluate configurations of your AWS resources for compliance and change management.

## Analytics

- **Amazon Kinesis Data Streams**: Real-time ingestion and processing of streaming data.
- **Amazon Kinesis Data Firehose**: Load streaming data into data stores like S3, Redshift, and Elasticsearch.
- **Amazon EMR**: Managed Hadoop and Spark framework for big data processing.
- **AWS Glue**: Serverless ETL service to discover, prepare, and combine data.
- **Amazon Athena**: Interactive query service to analyze data directly in S3 using SQL.
- **Amazon QuickSight**: Scalable BI service for creating and publishing interactive dashboards.

## Machine Learning & AI

- **Amazon SageMaker**: End-to-end ML platform for building, training, and deploying models.
- **Amazon Rekognition**: Image and video analysis for face recognition, object detection, and moderations.
- **Amazon Comprehend**: Natural language processing service for sentiment analysis, entity recognition, and topic modeling.
- **Amazon Polly**: Text-to-speech service that turns text into lifelike speech.
- **Amazon Lex**: Build conversational interfaces using voice and text (the technology behind Amazon Alexa).
- **Amazon Transcribe**: Automatic speech recognition to convert speech to text.
- **Amazon Translate**: Neural machine translation for translating text between languages.

## Migration & Transfer

- **AWS Database Migration Service (DMS)**: Migrate databases to AWS with minimal downtime.
- **AWS Snowball**: Petabyte-scale data transport solution using secure appliances.
- **AWS DataSync**: Automate and accelerate moving data between on-premises storage and AWS.
- **AWS Transfer Family**: Securely transfer files directly into and out of Amazon S3 or EFS using SFTP, FTPS, and FTP.

## Management & Governance

- **AWS Organizations**: Central governance and management across multiple AWS accounts.
- **AWS Control Tower**: Automate the setup of a secure, multi-account AWS environment.
- **AWS Service Catalog**: Create and manage catalogs of IT services for consistent provisioning.
- **AWS Budgets**: Set custom cost and usage budgets and receive alerts when thresholds are exceeded.


-----
