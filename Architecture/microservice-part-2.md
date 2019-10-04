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
#### Protobufs

### Service discovery
1. Service registry for service-service communication
2. Server-side discovery
3. Client-side discovery
4. Registration partterns

