# Data-intensive architecure

## A data-intensive application

Many applications today are data-intensive, as opposed to compute-intensive. Raw CPU power is rarely a limiting factor for these applications—bigger problems are usually the amount of data, the complexity of data, and the speed at which it is changing.

A data-intensive application is typically built from standard building blocks that provide commonly needed functionality. For example, many applications need to:

- Store data so that they, or another application, can find it again later (databases)

- Remember the result of an expensive operation, to speed up reads (caches)

- Allow users to search data by keyword or filter it in various ways (search indexes)

- Send a message to another process, to be handled asynchronously (stream processing)

- Periodically crunch a large amount of accumulated data (batch processing)

### three concerns that are important in most software systems:

`Reliability`
The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults, and even human error). See “Reliability”.

`Scalability`
As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth. See “Scalability”.

`Maintainability`
Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively. See “Maintainability”.

### Legacy system

Many people working on software systems dislike maintenance of so-called legacy systems—perhaps it involves fixing other people’s mistakes, or working with platforms that are now outdated, or systems that were forced to do things they were never intended for

## Storage and retrieval

### Data Structures of Database

Comparing characteristics of transaction processing versus analytic systems:

| Property             |       Transaction processing systems (OLTP)       |                   Analytic systems (OLAP) |
| -------------------- | :-----------------------------------------------: | ----------------------------------------: |
| Main read pattern    | Small number of records per query, fetched by key |    Aggregate over large number of records |
| Main write pattern   | Random-access, low-latency writes from user input |         Bulk import (ETL) or event stream |
| Primarily used by    |      End user/customer, via web application       |    Internal analyst, for decision support |
| What data represents |   Latest state of data (current point in time)    | History of events that happened over time |
| Dataset size         |              Gigabytes to terabytes               |                    Terabytes to petabytes |
