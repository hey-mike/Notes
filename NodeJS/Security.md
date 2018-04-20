# NodeJS security

## Code injection

- Indentify code injections
- Avoid shell injection

## Database injection

- Avoid SQL injection
- Mitigate injection attacks in NoSQL database

## Concurency

## Authendication

- Enforce password strenghth rules
- Move passowrd to server
- Password recovery
- And other authetication layers
  - Two factor authentication

## Session management

- Anonymize the sessionID
- Set time to live
- Re-create the session when the user logs in
- Bind the seesion to prevent hijacking

## Access control

## Deniel of service attack

- Avoid synchronous code
- Manage memory usage - read file size
- Avoid asymmetry

## Cross-site scripting (XSS)

1. Reflected XSS: which is a form of XSS where the injected script is reflected off the web server
2. Stored XSS: where the injected script is stored on the server and executes when rendering the web page.
3. DOM XSS (the fore two consider as server-side execution issues, this one is considerted as client-side execution)

- Prevent XSS through configuration of server
- Sanitize input foir relected/stored XSS
  - Escape unstrustred data inserted into HTML element content
    - Sanitize HTML with a libary
      - Bleach
      - Sanitizer
  - Escape untrusted data inserted into HTML attributes
  - Escape untrusted data inserted into JavaScript data values
    - Escape JSON values in an HTML context and read the data with JSON.Parse
  - Escape and validate untrusted data inserted into CSS property values
  - Escape untrusted data insered into HTML url parameter values
- Sanitize input for DOM XSS
  - Use DOM construction methods instead of HTML interpretation
  - JavaScript and HTML encode before HTML subcontext
  - Do not apply attribute encoding in DOM context
  - Avoid execution subcontexts
  - Do not apply css encoding in style context
  - JavaScript and url encode when creating links
 
