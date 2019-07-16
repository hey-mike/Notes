# Designing High Availability Architectures

## High availability compute

Measure HA using two metrics:

- RTO (Recovery Time Objective): This metric seeks to define the amount of time in which the recovery must be completed; for example, an RTO of 4 hours indicates that your solution must be restored to full functionality in 4 hours or less.

- RPO (Recovery Point Objective): This metric seeks to define the point to which data must be restored; this helps define how much data (for example) the organization is willing to lose; perhaps an organization is fine with losing 1 hour’s worth of email; in this case, the RPO could be stated as 1 hour.

### Fault tolerance(FT) is a subset of high availability(HA) solutions

FT seeks to create a zero downtime solution and zero performance degradation due to a component failure. With a completely effective FT solution the RTO and RPO values would both be 0.

### Non-VPC services (abstracted services) are almost all fault tolerant.

- if you are building a solution using EC2, you automatically need to build out at least two EC2 instances across AZs to accomplish what most of the AWS services do natively

### Services consideration

- using S3 to host media instead of putting the media on EC2/EBS solutions and replicating
- use Lambda to run cron processes versus an EC2 instance design running automation tasks

- **One improvement**: If you are designing an HA solution for your EC2-based architecture, a simple and effective method for improving upon your high availability is to leverage the global infrastructure of AWS. You can do this by placing key resources in different regions and/or Availability Zones.

- **geographic regions**: By provisioning EC2 instances in multiple geographic regions, you can launch Amazon EC2 instances in these regions, so your instances are closer to your customers.

- Each Region includes Availability Zones. Availability Zones are distinct locations that are engineered to be insulated from failures in other zones. They provide low latency network connectivity to other Availability Zones in the same region. **By launching EC2 instances in separate Availability Zones, you can protect your applications from any failures that might affect an entire Availability Zone**

- Elastic IP addresses are public IP addresses that can be programmatically mapped between EC2 instances within a Region.

## High Availability Application Services

- You can launch multiple EC2 instances from your AMI and then use Elastic Load Balancing to distribute incoming traffic for your application across these EC2 instances. This increases the availability of your application
- Placing your instances in multiple Availability Zones as done in the previous section also improves the fault tolerance in your application. If one Availability Zone experiences an outage, traffic is routed to the other Availability Zone.
- You can use EC2 Auto Scaling to maintain a minimum number of running instances for your application at all times.
  - EC2 Auto Scaling can detect when your instance or application is unhealthy and replace it automatically to maintain the availability of your application.
  - You can also use EC2 Auto Scaling to scale your EC2 capacity out or in automatically based on demand, using criteria that you specify.

## High Availability Database Services

Amazon recommends that you use Provisioned IOPS and DB instance classes (m1.large and larger) that are optimized for Provisioned IOPS for fast, consistent performance.

- In the event of a planned or unplanned outage of your DB instance, RDS automatically switches to a standby replica in another Availability Zone if you have enabled Multi-AZ
- The time it takes for the failover to complete depends on the database activity and other conditions at the time the primary DB instance became unavailable
- Failover times are typically 60–120 seconds
- Large transactions or a lengthy recovery process can increase failover time

The failover mechanism automatically changes the DNS record of the DB instance to point to the standby DB instance. As a result, **you need to re-establish any existing connections to your DB instance**. Because of the way the Java DNS caching mechanism works, you may need to reconfigure your JVM environment.

The primary DB instance switches over automatically to the standby replica if any of the following conditions occur:

- An Availability Zone has an outage.
- The primary DB instance fails.
- The DB instance’s server type is changed.
- The operating system of the DB instance is undergoing software patching.
- A manual failover of the DB instance was initiated using Reboot with failover.

Multi-AZ DB instance has failed over:

- You can set up DB event subscriptions to notify you via email or SMS that a failover has been initiated.
- You can view your DB events by using the RDS console or API actions.
- You can view the current state of your Multi-AZ deployment by using the RDS console and API actions.

## High Availability Networking Services

best practices:

- Leverage multiple dynamically routed, rather than statically routed, connections to AWS. This allows remote connections to fail over automatically between redundant connections. Dynamic routing also enables remote connections to automatically leverage available preferred routes, if applicable, to the on-premises network.

- Avoid relying on a single on-premises device, even if you were planning to use multiple interfaces for availability. Highly available connections require redundant hardware, even when connecting from the same physical location.

- When selecting AWS Direct Connect network service providers, consider a dual-vendor approach, if financially feasible, to ensure private-network diversity.

- Native Direct Connect can be established without a provider. A native Direct Connect deployment has the organization place its own hardware in an AWS partner data center. Customers would rack their own equipment. Separate Direct Connect equipment within the same partner data center could be requested, or separate data center connection points could also be requested. If a third-party provider is chosen for Direct Connect, at the very least ensure the partner has terminations in different data centers.

- Provision sufficient network capacity to ensure that the failure of one network connection does not overwhelm and degrade redundant connections.

## High Availability Storage Services

|                    |          S3 Standard           | S3 Standard-IA                 | S3 One Zone-IA | S3 Glacier                     |
| ------------------ | :----------------------------: | ------------------------------ | -------------- | ------------------------------ |
| Availability       |             99.99%             | 99.99%                         | 99.5%          | NA                             |
| Availability Zones | Greater than or equal to three | Greater than or equal to three | One            | Greater than or equal to three |

## High Availability Security Services

- authentication elements (such as an IAM user or role) and
- authorization elements (such as IAM policies) for a single application into multiple sets.
- you might take the application instances running behind a load balancer and designate a small set that you can use for production validation

## High Availability Monitoring Services

- CloudWatch
- Each Region is designed to be completely isolated from the other Regions, to achieve the greatest possible failure isolation and stability
- CloudWatch does not aggregate data across regions. Therefore, metrics are completely separate between regions, and you should consider this in your overall design.
