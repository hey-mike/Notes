# Microservice notes

## Domain-drive design

## Independent deploy, update, scale and replace

### Update

- Never share libraries between microservices
- Strong delimitation of microservice domains
- Establish a client-server relationship between microservices
- Deploy in separate containers

### Scale

**The Scale Cube**: 3 axis

- x-axis: horizontal decomposition: with the same application server replicated n times in full and in a balanced order of 1/n.
- y-axis: functional decomposition: a verb or route is used by the balancer to identify where to go with the request.
- z-axis: data partitioning: is very similar to the x-axis when it comes to scalability structure, as it distributes exactly the same code on each server. The big difference is that each server responds to a specific subset of dat
