# Angular Notes

Angular is consisted of six parts:

- Data Binding
- Directive (There are three kinds of directives in Angular)
  - Components — directives with a template.
    - are the most common of the three directives
  - Artribuite Directive
    - change the appearance or behaviour of an element, component, or another directive.
  - Structural Directive
    - change the DOM layout by adding and removing DOM elements.
    - i.e. iterator for components
- Forms
  - Template-driven forms
  - Reactive form
- Pipe
  - Applying data tranformation
- Service
  - Using Provider to apply Dependency Injection for service
- Module
  - Root module
  - Feature modules

## Design pattern

- NgRx is using Observable pattern
- Unidirectional Data Flow ( this is no really two way data-binding in angular 2)
- Dependency intejection

## Module

_imports_ This property is used to import the modules that are required by the classes in the modules.
_providers_ This property is used to define the module’s providers. When the feature module is
loaded, the set of providers are combined with those in the root module, which means
that the feature module’s services are available throughout the application (and not just
within the module).
_declarations_ This property is used to specify the directives, components, and pipes in the module.
This property must contain the classes that are used within the module and those that are
exposed by the module to the rest of the application.
_exports_ This property is used to define the public exports from the module. It contains some or all
of the directives, components, and pipes from the declarations property and some or all
of the modules from the imports property.

## RxJS

_next(value)_ This method creates a new event using the specified value.
_error(errorObject)_ This method reports an error, described using the argument, which can be any
object.
_complete()_ This method ends the sequence, indicating that no further events will be sent.

## in-memory-web-api.

it is used to simulate HTTP requests using data that has been defined locally. This provides a way to isolate a data source
class and ensure that only its behavior is being tested

## Test

_Jasmine.JS_ BDD test for Angular

- Define test component in testname.spec.ts
- Create test component
- describe test behaviour

## Router bug

https://stackoverflow.com/questions/38120756/angular2-router-navigate-refresh-page

Input type (type = "button) is important to make naviation animation works in angular 4, without specifying type, it works on IE11 and Edge browsers, but would reload the application in Chrome.
