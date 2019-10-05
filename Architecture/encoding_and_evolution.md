# Encoding and Evolution

## Formats for Encoding Data

1. In memory, data is kept in **objects, structs, lists, arrays, hash tables, trees**, and so on. These data structures are optimized for efficient access and manipulation by the CPU (typically using pointers).
2. When you want to write data to a file or send it over the network, you have to encode it as some kind of self-contained sequence of bytes (for example, **a JSON document**). Since a pointer wouldn’t make sense to any other process, this sequence-of-bytes representation looks quite different from the data structures that are normally used in memory.i
3. **Serialization** is unfortunately also used in the context of transactions, with a completely different meaning.

### Language-Specific Formats

1. The encoding is often tied to a particular programming language, and reading the data in another language is very difficult. If you store or transmit data in such an encoding, you are committing yourself to your current programming language for potentially a very long time, and precluding integrating your systems with those of other organizations (which may use different languages).

2. In order to restore data in the same object types, the decoding process needs to be able to instantiate arbitrary classes. This is frequently a source of security problems: if an attacker can get your application to decode an arbitrary byte sequence, they can instantiate arbitrary classes, which in turn often allows them to do terrible things such as remotely executing arbitrary code [6, 7].

3. Versioning data is often an afterthought in these libraries: as they are intended for quick and easy encoding of data, they often neglect the inconvenient problems of forward and backward compatibility.

4. Efficiency (CPU time taken to encode or decode, and the size of the encoded structure) is also often an afterthought. For example, Java’s built-in serialization is notorious for its bad performance and bloated encoding.

### JSON, XML, and Binary Variants

1. There is a lot of ambiguity around the encoding of numbers. **In XML and CSV, you cannot distinguish between a number and a string that happens to consist of digits** (except by referring to an external schema). **JSON distinguishes strings and numbers, but it doesn’t distinguish integers and floating-point numbers, and it doesn’t specify a precision.**

2. This is a problem when dealing with large numbers; **for example, integers greater than 253 cannot be exactly represented in an IEEE 754 double-precision floating-point number, so such numbers become inaccurate when parsed in a language that uses floating-point numbers (such as JavaScript)**. An example of numbers larger than 253 occurs on Twitter, which uses a 64-bit number to identify each tweet. The JSON returned by Twitter’s API includes tweet IDs twice, once as a JSON number and once as a decimal.

3. **JSON and XML have good support for Unicode character strings** (i.e., human-readable text), **but they don’t support binary strings (sequences of bytes without a character encoding)**. Binary strings are a useful feature, so people get around this limitation by encoding the binary data as text using Base64. The schema is then used to indicate that the value should be interpreted as Base64-encoded. This works, **but it’s somewhat hacky and increases the data size by 33%.**

4. There is optional schema support for both XML and JSON. These schema languages are quite powerful, and thus quite complicated to learn and implement. Use of XML schemas is fairly widespread, but many JSON-based tools don’t bother using schemas. Since the correct interpretation of data (such as numbers and binary strings) depends on information in the schema, applications that don’t use XML/JSON schemas need to potentially hardcode the appropriate encoding/decoding logic instead.

5. CSV does not have any schema, so it is up to the application to define the meaning of each row and column. If an application change adds a new row or column, you have to handle that change manually. CSV is also a quite vague format (what happens if a value contains a comma or a newline character?). Although its escaping rules have been formally specified, not all parsers implement them correctly.

### BINARY ENCODING

For data that is used only internally within your organization, there is less pressure to use a lowest-common-denominator encoding format. For example, **you could choose a format that is more compact or faster to parse**. For a small dataset, the gains are negligible, but once you get into the terabytes, the choice of data format can have a big impact. **JSON is less verbose than XML, but both still use a lot of space compared to binary formats**.

**Apache Thrift** and **Protocol Buffers** (protobuf) are binary encoding libraries that are based on the same principle. **Apache Avro** is another binary encoding format that is interestingly different from Protocol Buffers and Thrift.

## Modes of Dataflow

### Dataflow Through Databases

#### DIFFERENT VALUES WRITTEN AT DIFFERENT TIMES

- A database generally allows any value to be updated at any time. This means that within a single database you may have some values that were written five milliseconds ago, and some values that were written five years ago.
- When you deploy a new version of your application (of a server-side application, at least), you may entirely replace the old version with the new version within a few minutes
- Rewriting (migrating) data into a new schema is certainly possible, but it’s an expensive thing to do on a large dataset, so most databases avoid it if possible.

#### ARCHIVAL STORAGE

data dump will typically be encoded using the latest schema, even if the original encoding in the source database contained a mixture of schema versions from different eras. Since you’re copying the data anyway, you might as well encode the copy of the data consistently.

### Dataflow Through Services: REST and RPC

- **The web works this way**: clients (web browsers) make requests to web servers, making GET requests to download HTML, CSS, JavaScript, images, etc., and making POST requests to submit data to the server. The API consists of a standardized set of protocols and data formats (HTTP, URLs, SSL/TLS, HTML, etc.). Because web browsers, web servers, and website authors mostly agree on these standards, you can use any web browser to access any website (at least in theory!)
- a server can itself be a client to another service (for example, a typical web app server acts as client to a database). This approach is often used to **decompose a large application into smaller services by area of functionality**, such that one service makes a request to another when it requires some functionality or data from that other service. This way of building applications has traditionally been called a **service-oriented architecture (SOA)**, more recently refined and rebranded as **microservices** architecture
- services are similar to databases: they typically allow clients to submit and query data.However, while databases allow arbitrary queries using the query languages, services expose an application-specific API that only allows inputs and outputs that are predetermined by the **business logic (application code)** of the service . **This restriction provides a degree of encapsulation**: services can impose fine-grained restrictions on what clients can and cannot do.
- A **key design goal** of a service-oriented/microservices architecture is to make the application easier to change and maintain by making services independently deployable and evolvable

#### WEB SERVICES

When HTTP is used as the underlying protocol for talking to the service, it is **called a web service**.web services are not only used on the web, but in several different contexts:

1. A client application running on a user’s device (e.g., a native app on a mobile device, or JavaScript web app using Ajax) making requests to a service over HTTP. These requests typically go over the public internet.

2. One service making requests to another service owned by the same organization, often located within the same datacenter, as part of a service-oriented/microservices architecture. (Software that supports this kind of use case is sometimes called **middleware**.)

3. One service making requests to a service owned by a different organization, usually via the internet. This is used for data exchange between different organizations’ backend systems. This category includes public APIs provided by online services, such as credit card processing systems, or OAuth for shared access to user data.

> REST and SOAP

`REST` is not a protocol, but rather a design philosophy that builds upon the principles of HTTP It emphasizes simple data formats, using URLs for identifying resources and using HTTP features for **cache control, authentication, and content type negotiation**. REST has been gaining popularity compared to SOAP, **at least in the context of cross-organizational service integration**, and is often associated with microservices.An API designed according to the principles of REST is called **RESTful**.

`SOAP` is an XML-based protocol for making network API requests.The API of a SOAP web service is described using an XML-based language called the **Web Services Description Language(WSDL)**. WSDL enables code generation so that a client can access a remote service using local classes and method calls (which are encoded to XML messages and decoded again by the framework). **This is useful in statically typed programming languages, but less so in dynamically typed ones.**

> Problem of SOAP

- As WSDL is not designed to be human-readable, and as SOAP messages are often too complex to construct manually, users of SOAP rely heavily on tool support, code generation, and IDEs.For users of programming languages that are not supported by SOAP vendors, integration with SOAP services is difficult.
- Even though SOAP and its various extensions are ostensibly standardized, interoperability between different vendors’ implementations often causes problems

#### THE PROBLEMS WITH REMOTE PROCEDURE CALLS (RPCS)

The RPC model tries to make a request to a remote network service look the same as calling a function or method in your programming language, within the same process (this abstraction is called location transparency).

> **Problems**
>
> - A local function call is predictable and either succeeds or fails, depending only on parameters that are under your control. A network request is unpredictable: the request or response may be lost due to a network problem, or the remote machine may be slow or unavailable, and such problems are entirely outside of your control. Network problems are common, so you have to anticipate them, for example by retrying a failed request.
> - A local function call either returns a result, or throws an exception, or never returns (because it goes into an infinite loop or the process crashes). **A network request has another possible outcome: it may return without a result, due to a timeout**. In that case, you simply don’t know what happened: if you don’t get a response from the remote service, you have no way of knowing whether the request got through or not.
> - If you retry a failed network request, it could happen that the previous request actually got through, and only the response was lost. In that case, retrying will cause the action to be performed multiple times, unless you build a mechanism for deduplication (idempotence) into the protocol. Local function calls don’t have this problem. (We discuss idempotence in more detail in Chapter 11.)
> - Every time you call a local function, it normally takes about the same time to execute. A network request is much slower than a function call, and its latency is also wildly variable: at good times it may complete in less than a millisecond, but when the network is congested or the remote service is overloaded it may take many seconds to do exactly the same thing.
> - When you call a local function, you can efficiently pass it references (pointers) to objects in local memory. When you make a network request, all those parameters need to be encoded into a sequence of bytes that can be sent over the network. That’s okay if the parameters are primitives like numbers or strings, but quickly becomes problematic with larger objects.
> - The client and the service may be implemented in **different programming languages**, so the RPC framework must translate datatypes from one language into another. This can end up ugly, since not all languages have the same types—recall JavaScript’s problems with numbers greater than 253, for example (see “JSON, XML, and Binary Variants”). This problem doesn’t exist in a single process written in a single language.

> **Current development of PRC**
>
> Custom RPC protocols with a binary encoding format can achieve better performance than something generic like JSON over REST.
>
> However, a RESTful API has other significant advantages: it is good for experimentation and debugging (you can simply make requests to it using a web browser or the command-line tool curl, without any code generation or software installation), it is supported by all mainstream programming languages and platforms, and there is a vast ecosystem of tools available (servers, caches, load balancers, proxies, firewalls, monitoring, debugging tools, testing tools, etc.).
>
> For these reasons, REST seems to be the predominant style for public APIs. The main focus of RPC frameworks is on requests between services owned by the same organization, typically within the same data center.

> **DATA ENCODING AND EVOLUTION FOR RPC**
> The backward and forward compatibility properties of an RPC scheme are inherited from whatever encoding it uses:
>
> - Thrift, gRPC (Protocol Buffers), and Avro RPC can be evolved according to the compatibility rules of the respective encoding format.
> - In SOAP, requests and responses are specified with XML schemas. These can be evolved, but there are some subtle pitfalls .
> - RESTful APIs most commonly use JSON (without a formally specified schema) for responses, and JSON or URI-encoded/form-encoded request parameters for requests. Adding optional request parameters and adding new fields to response objects are usually considered changes that maintain compatibility.

#### Message-Passing Dataflow

Using a message broker has several advantages compared to direct RPC:

- It can act as a buffer if the recipient is unavailable or overloaded, and thus improve system reliability.

- It can automatically redeliver messages to a process that has crashed, and thus prevent messages from being lost.

- It avoids the sender needing to know the IP address and port number of the recipient (which is particularly useful in a cloud deployment where virtual machines often come and go).

- It allows one message to be sent to several recipients.

- It logically decouples the sender from the recipient (the sender just publishes messages and doesn’t care who consumes them).

However, a difference compared to RPC is that message-passing communication is usually one-way: a sender normally doesn’t expect to receive a reply to its messages. It is possible for a process to send a response, but this would usually be done on a separate channel. This communication pattern is asynchronous: the sender doesn’t wait for the message to be delivered, but simply sends it and then forgets about it.

> **MESSAGE BROKERS**
> The detailed delivery semantics vary by implementation and configuration, but in general, message brokers are used as follows: one process sends a message to a named queue or topic, and the broker ensures that the message is delivered to one or more consumers of or subscribers to that queue or topic. There can be many producers and many consumers on the same topic

> **DISTRIBUTED ACTOR FRAMEWORKS**
>
> - The **actor model** is a programming model for concurrency in a single process. Rather than dealing directly with threads (and the associated problems of race conditions, locking, and deadlock), logic is encapsulated in actors. Each actor typically represents one client or entity, it may have some local state (which is not shared with any other actor), and it communicates with other actors by sending and receiving asynchronous messages.Message delivery is not guaranteed: in certain error scenarios, messages will be lost. Since each actor processes only one message at a time, it doesn’t need to worry about threads, and each actor can be scheduled independently by the framework.
> - In **distributed actor frameworks**, this programming model is used to scale an application across multiple nodes. The same message-passing mechanism is used, no matter whether the sender and recipient are on the same node or different nodes. If they are on different nodes, the message is transparently encoded into a byte sequence, sent over the network, and decoded on the other side.
