# Microservice notes

## What are microservices?

### Principles and characteristics

1. No monolithic modules
2. Dumb communication pipes
3. Decentralization or self-governance
4. Service contracts and statelessness
5. Lightweith
6. Polylog

### Good parts of microservices

1. self-dependent teams
2. Graceful degration of services
3. Supports polygolt architecture and DevOps
4. Event-driven architecture

### Bad and challenge parts

1. Organization and orchestration
2. Platform
3. Testing
4. Service discovery

### Twelve-factor application

1. **Codebase**: We maintain a single code base here for each microservice, with a configuration specific to their own environments, such as development, QA, and prod. Each microservice would have its own repository in a version control system such as Git, mercurial, and so on.
2. **Dependencies**: All microservices will have their dependencies as part of the application bundle. In Node.js, there is package.json, which mentions all the development dependencies and overall dependencies. We can even have a private repository from where dependencies will be pulled.
3. **Configs**: All configurations should be externalized, based on the server environment. There should be a separation of config from code. You can set environment variables in Node.js or use Docker compose to define other variables.
4. **Backing services**: Any service consumed over the network such as database, I/O operations, messaging queries, SMTP, the cache will be exposed as microservices and using Docker compose and be independent of the application.
5. **Build, release, and run**: We will use automated tools like Docker and Git in distributed systems. Using Docker we can isolate all the three phases using its push, pull, and run commands.
6. **Processes**: Microservices designed would be stateless and would share nothing, hence enabling zero fault tolerance and easy scaling. Volumes will be used to persist data thus avoiding data loss.
7. **Port binding**: Microservices should be autonomous and self-contained. Microservices should embed service listeners as part of service itself. For example— in Node.js application using HTTP module, service network exposing services for handling ports for all processes.
8. **Concurrency**: Microservices will be scaled out via replication. Microservices are scaled out rather than scaled up. Microservices can be scaled or shrunk based on the flow of workload diversity. Concurrency will be dynamically maintained.
9. **Disposability**: To maximize the robustness of application with fast startup and graceful shutdown. Various options include restart policies, orchestration using Docker swarm, reverse proxy, and load balancing with service containers.
10. **Dev/prod parity**: Keep development/production/staging environments exactly alike. Using containerized microservices helps via build once, run anywhere strategy. The same image is deployed across various DevOps stage.
11. **Logs**: Creating separate microservice for logs for making it centralized, to treat as event streams and send it to frameworks such as elastic stack (ELK).
12. **Admin processes**: Admin or any management tasks should be packed as one of the processes, so they can be easily executed, monitored, and managed. This will include tasks like database migrations, one-time scripts, fixing bad data, and so on.

### Communication between microservices

#### Remote Procedure Invocation (PRI) - Apache Thrift and Google's gRPC

RPI uses binary rather than text to keep the payload very compact and efficient. These requests are multiplexed over a single TCP connection, which can allow multiple concurrent messages to be in flight without having to compromise for network consumption usage.

Pros:

1. Request and reply are easy
2. Simple to maintain as there is no middle broker
3. Bidirectional streams with HTTP/2-based transportation methods
4. Efficiently connecting polyglot services in microservices styled architectural ecosystems

Cons:

1. The caller needs to know the locations of service instances, that is, maintain a client-side registry and server-side registry
2. It only supports the request and reply model and has no support for other patterns such as notifications, async responses, the publish/subscribe pattern, publish async responses, streams, and so on

#### Messaging and message bus

Route messages coming from various clients to different microservices destinations. Changes messages to desired transformations as per need. Ability to do message aggregations, segregate a message into multiple messages, and send them to the destination as per need and recompose them. Respond to errors or events. Provide content and routing using the publish-subscribe pattern.

Pros:

1. The client is decoupled from the services; they don't need to discover any services. Loosely coupled architecture throughout.
2. Highly available as the message broker persists messages until the consumer is able to process them for operations.
3. It has support for a variety of communication patterns, including the widely used request/reply, notifications, async responses, publish-subscribe, and so on.

#### Protobufs

**Protocol buffers** or **protobufs** are a binary format created by Google.Some demonstrations effectively show that protobufs is six times faster than JSON.

> Pros:
>
> - Formats for protobufs are self-explaining—formal formats.
> - It has RPC support; you can declare server RPC interfaces as part of protocol files.
> - It has an option for structure validation. As it has larger datatype messages that are serialized on protobufs, it can be validated automatically by the code that is responsible for exchanging them.

> Cons:
>
> - It is an upcoming pattern; hence you won't find many resources or detailed documentation for implementation of protobuf. If you just look for the protobuf tag on Stack Overflow, you will merely see a mere 10,000 questions.
> - As it's binary format, it's non-readable when compared to JSON, which is simple to read and analyze on the other hand. The next generation of protobuf and flatbuffer is already available now.

### Service discovery

#### Service registry for service-service communication

1. `etcd`: A key-value store used for shared configuration and service discovery. Projects such as Kubernates and cloud foundry are based on etcd as it can be highly available, key-value based, and consistent.
2. `consul`: Yet another tool for service discovery. It has wide options such as exposed API endpoints that allow the client to register and discover services and perform health checks to determine service availability.
3. `ZooKeeper`: Very widely used, highly available, and a high performant coordinated service used in distributed applications. Originally a subproject of Hadoop, Zookeeper is a widely used top-level project and it comes preconfigured with various frameworks.

#### Server-side discovery

All requests made to any of the services are routed via a router or load balancers that run in a location known to client interfaces. The router then queries a maintained registry and forwards the request based on the query response

Pros:

1. The client does not need to know the location of different microservices. They just need to know the location of the router and the service discovery logic is completely abstracted from the client so there is zero logic at the client end.
2. Some environments provide this component functionality for free.

Cons:

1. It has more network hops, that is, one from the client service registry and another from the service registry microservice.
2. If the load balancer is not provided by the environment, then it has to be set up and managed. If not properly handled, then it can be a single point of failure.
3. The selected router or load balancer must support different communication protocols for modes of communication.

#### Client-side discovery

Under this mode of discovery, the client is responsible for handling the network location of available microservices and load balancing incoming requests across them. The client needs to query a service registry (a database of available services maintained on the client side). The client then selects service instances on the basis of an algorithm and then makes a request
Netflix uses this pattern extensively and has open sourced their tools **Netflix OSS, Netflix Eureka, Netflix Ribbon, and Netflix Prana**. Using this pattern has the following advantages:

1. High performance and availability as there are fewer transition hops, that is, the client just has to invoke the registry and the registry will redirect to the microservice as per their needs.
2. This pattern is fairly simple and highly resilient as besides the service registry there are no moving parts. As the client knows about available microservices, they can make intelligent decisions easily such as to use a hash, when to trigger auto-scaling, and so on.
3. **One significant drawback** of using this mode of service discovery is implementation of client-side service discovery logic has to be done in every programming language of the framework that is used by the service clients. For example, Java, JavaScript, Scala, Node.js, Ruby, and so on.

#### Registration partterns

While using this pattern, any microservice instance is responsible for registering and deregistering itself from the maintained service registry. To maintain health checks, a service instance sends heartbeat requests to prevent its registry from expiring.

Pros:

- It couples the service tightly to the self-service registry, which forces us to enable the service registration code in each language we are using in the framework
- Any microservice that is in running mode, but is not able to handle requests, will often be unaware of which state to pursue, and will often end up forgetting to unregister from the registry

### Data management

#### Database per service

- **Private tables/collections per service**: Each microservice has a set of defined tables or collections that can only be accessed by that service
- **Schema per service**: Each service has a schema that can only be accessed via the microservice it is bound to
- **Database per service**: Each microservice maintains its own database as per its needs and requirements

Pros:

- Loosely coupled services that can stand on their own; changes to one service's datastore won't affect any other services.
  Each service has the liberty to select the datastore as required.
- Each microservice has the option of whether to go for relational or non-relational databases as per need. For example, any service that needs intensive search results on text may go for **Solr** or **Elasticsearch**, whereas any service where there is structured data may go for any SQL database.

Cons:

- Handling complex scenarios that involve transactions spanning across multiple services. The CAP theorem states that it is impossible to have more than two out of the following three guarantees—consistency, availability, and partitions in the distributed datastore, so transactions are generally avoided.
- Queries ranging across multiple databases are challenging and resource consuming.
- The complexity of managing multiple SQL and non-SQL datastores.

To overcome the drawbacks, the following patterns are used while maintaining a database per service:

- **Sagas**: A saga is defined as a batch sequence of local transactions. Each entry in the batch updates the specified database and moves on by publishing a message or triggering an event for the next entry in the batch to happen. If any entry in the batch fails locally or any business rule is violated, then the saga executes a series of compensating transactions that compensate or undo the changes that were made by the saga batch updates.
- **API Composition:** This pattern insists that the application should perform the join rather than the database. As an example, a service is dedicated to query composition. So, if we want to fetch monthly product distributions, then we first retrieve the products from the product service and then query the distribution service to return the distribution information of the retrieved products.
- **Command Query Responsibility Segregation (CQRS)**: The principle of this pattern is to have one or more evolving views, which usually have data coming from various services. Fundamentally, it splits the application into two parts—the command or the operating side and the query or the executor side. It is more of a publisher-subscriber pattern where the command side operates create/update/delete requests and emits events whenever the data changes. The executor side listens for those events and handles those queries by maintaining views that are kept up to date, based on the subscription of events that are emitted by the command or operating side.
