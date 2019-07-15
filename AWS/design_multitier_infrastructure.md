# Designing a Multitier Infrastructure

## SINGLE-TIER ARCHITECTURES

It is a simple architecture in which all the required components for a software application or technology are provided on a single server or platform.

- A web server
- The end-user interface
- Middleware required to run the logic of the application (beyond what the underlying OS can provide)
- Back-end data required for the application

Advantages

- It is simple to understand and design.
- It is easy to deploy.
- It is easy to administer.
- It has potentially lower costs associated with it.
- It can be easy to test.
- It is often ideal for environments that do not require scalability.

## MULTITIER ARCHITECTURES

Advantages

- Improved security
- Improved performance
- Improved scalability
- Fine-grained management
- Fine-grained maintenance
- Higher availability
- Promotes decoupling of components
- Promotes multiple teams for architecture development, implementation, and maintenance

### Sample Components of an AWS Multitier Architecture

| Requirement              |           Service            |
| ------------------------ | :--------------------------: |
| DNS Resolution           |           Route 53           |
| Content Delivery Network |          CloudFront          |
| Web Resources            |    Simple Storage Service    |
| Web Servers              |    Elastic Compute Cloud     |
| Load Balancing           |    Elastic Load Balancing    |
| Scalability              |         Auto Scaling         |
| Application Servers      |    Elastic Compute Cloud     |
| Database Servers         | Relational Database Services |

- DNS resolution of client requests is handled by Route 53. This service helps route traffic requests to and from clients to the correct AWS services for the application and to the correct internal infrastructure components within the AWS data centers. Route 53 features vast scalability and high availability for this task.

- Content from your application (streaming, static, and/or dynamic) can be delivered through CloudFront. CloudFront provides an impressive global network of edge locations. CloudFront can help ensure that client requests are automatically routed to the nearest edge location so that content can be delivered with the lowest possible latency.

- S3 can provide valuable object-based storage for your multitier architecture. This might even include the static content required by any web content required for your solution.

- Elastic Load Balancing can handle HTTP requests to distribute them between multiple EC2 instances. Note that these EC2 instances can be strategically located across different Availability Zones to increase availability. Also note that the ELB service can dramatically increase the fault tolerance of your solution.

- EC2 instances can function as the web servers in a web-based application. An AMI is chosen that facilitates such web services.

- An Auto Scaling group can be used for the web servers to facilitate scalability. This allows the automatic expansion of instances when requests spike and can even eliminate instances when they are not needed to help save on costs.

- Amazon RDS can provide the data required for the application. To help with high availability, the database servers can be located in different Availability Zones. Synchronous replication can be used between these servers to ensure accurate data in all of them.

## THE CLASSIC THREE-TIER ARCHITECTURE

- Presentation tier: Consists of the components that users interact with, which might include web pages and/or mobile app user interface components. The Amazon **Cognito service** can assist with the **creation and management of user identities**. **S3** might be the source of any **static web content** you need to store and then deliver for the tier. The **API Gateway** can be **enabled for cross-origin resource sharing compliance**. This permits web browsers to invoke APIs from within your static web pages.

- Logic tier: Contains the code required to translate user actions initiated at the presentation tier to the functionality required by the application: This certainly lends itself to the power of the API Gateway and Lambda functionality. They combine to allow a revolutionary new serverless approach to the multitier architecture. Thanks to **advantages that come with serverless implementations**, new levels of h**igh availability, scalability, and security** are possible. While a more traditional server-based implementation of the three-tier architecture might require thousands of servers in order to scale, a serverless environment does not need a single virtual server in its operation.

- Data tier: Consists of storage media that hold the data relevant for the application architecture, which might be database, object stores, caches, or file systems

### data tier of your architecture

The data tier of your architecture can be used with a wide variety of AWS solutions. They are often organized into two broad categories: Amazon VPC-hosted data stores and IAM-enabled data stores.

**VPC-hosted data store options include:**

- RDS: Provides several relational database engine options

- ElastiCache: Boosts performance with in-memory caching

- Redshift: Provides simple data warehousing capabilities

- EC2: Provides data stored within technology offered by an EC2 instance(s)

**IAM-enabled options include:**

- DynamoDB: An infinitely scalable NoSQL database

- S3: Infinitely scalable object-based storage

- Elastisearch Service: A managed version of the popular search and analytics engine called Elastisearch
