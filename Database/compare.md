## What are common use cases for MongoDB?

MongoDB is a general purpose database that is used for a variety of use cases. The most common use cases for MongoDB include Single View, Internet of Things, Mobile, Real-Time Analytics, Personalization, Catalog, and Content Management.

## When would MySQL be a better fit?

While most modern applications require a flexible, scalable system like MongoDB, there are use cases for which a relational database like MySQL would be better suited. Applications that require complex, multi-row transactions (e.g., a double-entry bookkeeping system) would be good examples. MongoDB is not a drop-in replacement for legacy applications built around the relational data model and SQL.

A concrete example would be the booking engine behind a travel reservation system, which also typically involves complex transactions. While the core booking engine might run on MySQL, those parts of the app that engage with users – serving up content, integrating with social networks, managing sessions – would be better placed in MongoDB
