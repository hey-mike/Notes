# Designing for Elasticity

## ELASTIC LOAD BALANCING

- Elastic Load Balancing (ELB) distributes incoming application or network traffic across multiple targets. These targets are AWS resources such as Amazon EC2 instances, containers, and IP addresses. To foster high availability, ensure the resources are in multiple Availability Zones.
- Elastic Load Balancing scales your load balancer as traffic to your application changes over time and can scale to a majority of workloads automatically. You can add and remove compute resources from your load balancer as your needs change, without disrupting the overall flow of requests to your applications.
- You can configure health checks, which are used to monitor the health of the computing resources so that the load balancer can send requests only to the healthy ones. You can also offload the work of SSL/TLS encryption and decryption to your load balancer so that your compute resources can focus on their main work.

## three types of load balancers

- Application Load Balancers, Network Load Balancers, and Classic Load Balancers.

It supports applications:

- **EC2**: These virtual servers run your applications in the cloud. You can configure your load balancer to route traffic to your EC2 instances.

- **ECS**: This service enables you to run, stop, and manage Docker containers on a cluster of EC2 instances. You can configure your load balancer to route traffic to your containers.

- **Auto Scaling**: This service ensures that you are running your desired number of instances, even if an instance fails, and enables you to automatically increase or decrease the number of instances as the demand on your instances changes. If you enable Auto Scaling with Elastic Load Balancing, instances that are launched by Auto Scaling are automatically registered with the load balancer, and instances that are terminated by Auto Scaling are automatically deregistered from the load balancer.

- **CloudWatch**: This service enables you to monitor your load balancer and take action as needed.

- **Route 53**: This service provides a reliable and cost-effective way to route visitors to websites by translating domain names (such as www.ajsnetworking.com) into the numeric IP addresses (such as 69.163.163.123) that computers use to connect to each other. AWS assigns URLs to your resources, such as load balancers. However, you might want a URL that is easy for users to remember. For example, you can map your domain name to a load balancer.

## AUTO SCALING

It supports applications:

- EC2 Auto Scaling groups

- Aurora DB clusters

- DynamoDB global secondary indexes

- DynamoDB tables

- ECS services

- Spot Fleet requests

### Target Tracking Scaling Policies

- keeping the metric close to the target value, a target tracking scaling policy also adjusts to changes in the metric due to a changing load pattern and minimizes changes to the capacity of the scalable target.
  > When discussing scaling the resources of a service, we are scaling those resources horizontally (out and in with elasticity), while the service made up of those resources is being scaled up and down (vertically because the single service is getting bigger or smaller). A single service scales both up and down and out and in, depending on the context.

### Things to keep in mind

- You cannot create target tracking scaling policies for Amazon EMR clusters or AppStream 2.0 fleets.

- You can create 50 scaling policies per scalable target. This includes both step scaling policies and target tracking policies.

- A target tracking scaling policy assumes that it should perform scale-out when the specified metric is above the target value. You cannot use a target tracking scaling policy to scale out when the specified metric is below the target value.

- A target tracking scaling policy does not perform scaling when the specified metric has insufficient data. It does not perform scale-in because it does not interpret insufficient data as low utilization. To scale in when a metric has insufficient data, create a step scaling policy and have an alarm invoke the scaling policy when it changes to the INSUFFICIENT_DATA state.

- You may see gaps between the target value and the actual metric data points. The reason is that Application Auto Scaling always acts conservatively by rounding up or down when it determines how much capacity to add or remove. This prevents it from adding insufficient capacity or removing too much capacity. However, for a scalable target with small capacity, the actual metric data points might seem far from the target value. For a scalable target with larger capacity, adding or removing capacity causes less of a gap between the target value and the actual metric data points.

- We recommend that you scale based on metrics with a 1-minute frequency because that ensures a faster response to utilization changes. Scaling on metrics with a 5-minute frequency can result in slower response time and scaling on stale metric data.

- To ensure application availability, Application Auto Scaling scales out proportionally to the metric as fast as it can but scales in more gradually.

- Do not edit or delete the CloudWatch alarms that Application Auto Scaling manages for a target tracking scaling policy. Application Auto Scaling deletes the alarms automatically when you delete the Auto Scaling policy.

### The Cooldown Period

- **scale-out cooldown period**, the intention is to continuously scale out.
- **scale-in cooldown period**, the intention is to scale in conservatively to protect your application’s availability. If another alarm triggers a scale-out policy during the cooldown period after a scale-in event, Application Auto Scaling scales out your scalable target immediately.
