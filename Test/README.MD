# Notes for test

## Unit test

The unit tests are used to prove the smallest testable part of a computer program.In this sense, the great challenge is to write code that is testable; otherwise, it will be impossible to apply the unit tests.

When we create the unit test, we have to use a mechanism so that the function test does not touch the database. The mechanism is commonly known as a **mock**.When applying a mock to the unit test, we isolate the function we want to test, then any possible changes in the database will not create conflict in the unit test scenarios.

## Integration tests

Like unit tests, integration tests must also be deterministic, but they do not prove only an isolated segment of the code. Integration tests, in the case of microservices, will validate the entire flow from the starting point of the test to the last interaction; it could be a vendor app or a database, as an example.

## End-to-end tests

The end-to-end tests are conceptually similar to integration tests, but they validate the entire business flow of the application. The main purpose of this type of test is to check whether any flow stages are corrupted. Many developers get confused about the difference between end-to-end and integration tests.

examples:

1. Create a user.
1. Create a news article for each type of news service (famous, politics, and sports).
1. Search for all news articles created in the test by sending the user_id function in the request cookie.
1. Validate the recommendations created for the user.

## Signature tests

Imagine a scenario where we have several development teams working on different microservices of the same application. These microservices have some communication between them; there is a kind of contract between them that is the payload of the microservice, also known as the **Service Signature**. One of the development teams modifies the signature of the microservice causing errors in other parts of the application.

When a microservice has the signature changed, a task must be generated for the other development teams responsible for microservices that integrate with this signature.

## Monkey tests

Monkey tests are usually automated tests with random values that target identified errors in the application. Normally, the errors that emerge in this type of test are due to a failure of treatment in the input or slowness in the treatment of input owing to the stress of the application.

In general, the monkey test is useful for identifying out-of-the-box errors.

**Chaos Monkey** has the following test categories:

- Chaos Gorilla: This simulates the unavailability of an entire zone of availability
- Conformity Monkey: This closes instances that do not adhere to best practices
- Doctor Monkey: This performs performance checks (similar to a CPU)
- Janitor Monkey: This searches for unused resources and deletes them
- Latency Monkey: This creates artificial delays in client-server communication
- Security Monkey: This encounters security vulnerabilities, such as non-security groups configured properly
