# design decouple mechanisms

## Foundation

- Decoupling\*\*: components remaining potentially autonomous and unaware of each other as they complete their work for some greater output. This decoupling can be used to describe components that make up a simple application, and the term even applies on a broad scale

### Advantages of decoupling

- To help ensure changes or failures in one component have a minimal effect on others.

- To have well-defined interfaces that allow the various components to interact with each other only through specific, technology-agnostic interfaces. The ability to modify any underlying operations without affecting other components should be made possible.

- To enable smaller services to be consumed without prior knowledge of their network topology details through loose coupling. This enables you to launch or terminate new components at any point.

- To reduce the impact on the end users and increase your ability to make progress on your offline procedures.

### Synchronous decoupling

An example of synchronous decoupling in AWS is using Elastic Load Balancing (ELB) to distribute traffic between EC2 instances that are hosted in multiple Availability Zones.

### Asynchronous decoupling

An example of asynchronous decoupling is using the Simple Queue Service (SQS) to handle messaging between components.An example of asynchronous decoupling is using the Simple Queue Service (SQS) to handle messaging between components.
