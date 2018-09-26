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

## Module
- AMD: AMD stands for Asynchronous Module Definition. This system works in such a way that when the module is defined, usually at the moment of loading the file with the source code, it is not necessary when it is going to be used, but rather when it is available for later use in the system.
- CommonJS: Unlike AMD modules that are loaded asynchronously on demand, CommonJS modules are loaded synchronously

## Pure function vs impure function
**Pure function**
- Must return something
- No matter how many times the function is executed the result should be the same if the input is also the same
- Input data must not be mutated during the execution of the function
- Not iterate over any array using for, while, do-while...
- Not sharing any state with other functions
- Implementing it should not have any side-effects in any other part of our program