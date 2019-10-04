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

**Apache Thrift**  and **Protocol Buffers** (protobuf)  are binary encoding libraries that are based on the same principle. **Apache Avro** is another binary encoding format that is interestingly different from Protocol Buffers and Thrift.