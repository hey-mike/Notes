# Notes for NodeJS

## Asynchronous batching and caching

**Batching**
If we are invoking an asynchronous function while there is still another one pending, we can attach callback to the already running operation, instead of creating a brand new request.

Problems:
The faster the API, the fewer batched requests we get. Alought the API is fast enough, it still represents a factor in the resource load of an application.
Also, sometimes we can safely assume that the result of an API invocation will not change so often; therefore, a simple request batching willl not provide the best performance. In all these circumstances, the best candidate to reduce the load of an application and increase its responsiveness is definitely a more agressive caching pattern.

**Catching**
As soon as a request completes, we store its result in the catch, which can be a variable, an entry in the database, or in a specialized catching server. Hence, the next time the API is invoked, the result can be retrieved immediately from the cache, insead of spawning another request.

## Running CPU-bound tasks

## Scalability

**Three dimesions**
x-axis: Cloning
y-axis: Decomposing by service/functionality
z-axis: Splitting by data partition

vertical scaling - adding more resources to a single machine
horizontal scaling - adding more machines to the infrastructure

**Cloning**
