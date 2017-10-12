# Angular Notes

Angular is consisted of six parts:
- Data Binding
- Directive
  - Built-in Directive
  - Artribuite Directive
  - Structural Directive - i.e. iterator for components
- Component
- Pipe
  - Applying data tranformation
- Service
  - Using Provider to apply Dependency Injection for service
- Module
  - Root module
  - Feature modules




## Module
*imports* This property is used to import the modules that are required by the classes in the modules.
*providers* This property is used to define the module’s providers. When the feature module is
loaded, the set of providers are combined with those in the root module, which means
that the feature module’s services are available throughout the application (and not just
within the module).
*declarations* This property is used to specify the directives, components, and pipes in the module.
This property must contain the classes that are used within the module and those that are
exposed by the module to the rest of the application.
*exports* This property is used to define the public exports from the module. It contains some or all
of the directives, components, and pipes from the declarations property and some or all
of the modules from the imports property.
