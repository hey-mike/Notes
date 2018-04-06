# JavaScript notes 

## comparasion

- Plain JavaScript 
  - pros: 
    - Does not require any additional libraries or technology
    - Offers the best performance
    - Provides the best level of compatibility with third-party libraries
    - Allows the creation of ad hoc and more advanced algorithms
  - cons:
    - Might require extra code and relatively complex algorithms
- Async(lib)
  - pros:
    - Simplifies the most common control flow patterns
    - Is still a callback-based solution
    - Good performance
  - cons:
    - Introduce an extreanl dependency 
    - Might still not be enough for advanced flows
- Promises
  - pros:
    - Greatly simplifies the most common control flow patterns
    - Robust error handling
    - Part of the ES2015 specification
    - Guarantees deferred invocation of onFulfilled and onRejected
  - cons:
    - Requires promisify callback-based APIs
    - Intoduces a small performance hit
- Generators
  - pros:
    - Makes non-blocking API look like a blocking one
    - Simplifies erro handling
    - Part of ES2015 specification
  - cons:
    - Requires a complementary control flow library
    - Still requires callbacks or promises to implement non-sequential flows
    - Requires thunkify or promisify nongenerator-bnased APIs
- Async await
  - pros:
    - Makes non-blocking API look like blocking
    - Clean and intuitive syntax

## Warning:
With `let` and `const` in ES6, it’s no longer safe to check for an identifier’s existence using `typeof`:

