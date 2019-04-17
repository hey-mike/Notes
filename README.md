# General Notes

Search Method

- _Soundex_ is a phonetic algorithm for indexing names by sound as pronounced in English. It is appropriate when you want to do name lookups and allow users to find correct results despite minor differences in spelling.

- _Fuzzy matching_ is the technique of finding strings that match a string, approximately, not exactly. The closeness of a match is measured in terms of operations necessary to convert the string into an exact match.

- _Levenshtein_. It's a simple algorithm that provides good results, but it's not supported by MongoDB. Measuring the Levenshtein distance must thus be done by fetching the entire result set and then applying the algorithm for the search query on all the strings. The speed of the operation grows linearly with the number of documents in your database, so unless you have a very small document set, this is most likely not
  worth doing

Website Documentation
http://patternlab.io/

# OAuth2

## Roles

Resource Owner: User

The resource owner is the user who authorizes an application to access their account. The application's access to the user's account is limited to the "scope" of the authorization granted (e.g. read or write access).

Resource / Authorization Server: API

The resource server hosts the protected user accounts, and the authorization server verifies the identity of the user then issues access tokens to the application.

From an application developer's point of view, a service's API fulfills both the resource and authorization server roles. We will refer to both of these roles combined, as the Service or API role.

Client: Application

The client is the application that wants to access the user's account. Before it may do so, it must be authorized by the user, and the authorization must be validated by the API.

## Abstract Protocol Flow

1. The application requests authorization to access service resources from the user
2. If the user authorized the request, the application receives an authorization grant
3. The application requests an access token from the authorization server (API) by presenting authentication of its own identity, and the authorization grant
4. If the application identity is authenticated and the authorization grant is valid, the authorization server (API) issues an access token to the application. Authorization is complete.
5. The application requests the resource from the resource server (API) and presents the access token for authentication
6. If the access token is valid, the resource server (API) serves the resource to the application

## Multipart upload

Multipart upload allows you to upload a single object as a set of parts. Each part is a contiguous portion of the object's data. You can upload these object parts independently and in any order. If transmission of any part fails, you can retransmit that part without affecting other parts. After all parts of your object are uploaded, Amazon S3 assembles these parts and creates the object. In general, when your **object size reaches 100 MB**, you should consider using multipart uploads instead of uploading the object in a single operation.

## Reading list (2017)

- Learning Scrapy
- Vrtual Development enviroment Cookbook
- Pro MERN stack
- Python Machine Learning
- Hands-on Machine Learning with scikit-learn and Tensorflow
- Creating Development Environments with Vagrant, Second Edition
- Developing Microservices with Node.js
- Express in Action
- Pro Angular, 2nd Edition
- Pro REST API Development with Node.js
- Pro RESTful APIs
- Reactive Programming with Node.js
- Vagrant Virtual Development Environment Cookbook
- Introduction to Machine Learning with Python
- Real-World Machine Learning
- Web 2.0 Architectures

## Reading list (2018)

- Node.js 8 the Right Way
- Building Microservices
- Node.js Design Patterns - second edition
- Mastering Node.js - second edition
- Secure Your Node.js Web Application
- Pro .NET core MVC 2
- Pro Angular 2nd edition
- Clean Architecture
- Essential C# 7.0, six edition
- ASP.NET Core with Angular
- React Design patterns and Best Practices
- How to Kill the Scrum Monster: Quick Start to Agile Scrum Methodology and the Scrum Master Role
- Redux in Action
- React and React Native
- React 16 Tooling
- Pro Angular 6
- Hands-On Microservices with Node.js
- Microservice Patterns and Best Practices

## Reading list (2019)

- Hands-On Full-Stack Web Development with GraphQL and React
- Clean Architecture: A Craftsman's Guide to Software Structure and Design, First Edition
- Designing Data-Intensive Applications
- IOS 11 Programming with SWIFT: Develop iOS mobile applications from scratch
- Hands-on Resful Service With TypeScript 3
- Information Security: Principles and Practies, Second edition

## Reading queue

- The Nature of Software Development
- Your Code as a Crime Scene
