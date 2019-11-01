# Microservice communication

## Communication types

### Two axis

The first axis defines if the protocol is synchronous or asynchronous:

- **Synchronous protocol:** HTTP is a synchronous protocol.

  - The client sends a request and waits for a response from the service. That's independent of the client code execution that could be synchronous (thread is blocked) or asynchronous (thread isn't blocked, and the response will reach a callback eventually). The important point here is that the **protocol (HTTP/HTTPS) is synchronous and the client code can only continue its task when it receives the HTTP server response.** and **Web API**is the common type of using this communication
  - **All request / response cycle consider to be a nti-pattern**

- **Asynchronous protocol:** the protocols like AMQP (a protocol supported by many operating systems and cloud environments) use asynchronous messages.
  - The client code or message sender usually doesn't wait for a response. It just sends the message as when sending a message to a RabbitMQ queue or any other message broker.( **AMQP**, **Http Polling**)

The second axis defines if the communication has a single receiver or multiple receivers:

- **Single receiver**. Each request must be processed by exactly one receiver or service. An example of this communication is the Command pattern.

- **Multiple receivers**. Each request can be processed by zero to multiple receivers. **This type of communication must be asynchronous**. An example is the publish/subscribe mechanism used in patterns like Event-driven architecture. This is based on an event-bus interface or message broker when propagating data updates between multiple microservices through events; it's usually implemented through a service bus or similar artifact like Azure Service Bus by using topics and subscriptions.

## Communication styles
