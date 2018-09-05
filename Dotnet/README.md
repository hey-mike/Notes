# Dotnet notes

## Dotnet MVC

## Dotnet API

## Duck Typing

## Install Angular 5 app with dotnet cli

1. Installl the templates

```bash
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0-rc1-final
```

2. Create a new Angular App

```bash
dotnet new angular -o ProjectName
```

3. Change Enviroment variable to "Development"

```bash
SET ASPNETCORE_Environment=Development
```

4. Buidl the application

```bash
dotnet build
```

Or 

```

ASPNETCORE_ENVIRONMENT=Development dotnet watch run

## migrate a database
**Code-First** Migrations: giving the developer a chance to alter the Database schema without having to drop/recreate the whole thing in Production.

``` bash
dotnet ef migrations add "Identity" -o "Data/Migrations"
```

## update a database

- option 1: update

```bash
dotnet ef database update
```

- option 2: drop and recreate

```bash
dotnet ef database drop
dotnet ef database update
```
```
ASPNETCORE_ENVIRONMENT=Development dotnet run
```

### Depency injection
| Name                                                                                          | Description                                                                                                                                                                                                                                                                                                                                                          |
|-----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AddTransient<service,implType>()                                                              | This method tells the service provider to create a new instance of the implementation type for every dependency on the service type. See the “Using the Transient Life Cycle” section.                                                                                                                                                                               |
| AddTransient<service>()                                                                       | This method is used to register a single type, which will be instantiated for every dependency, as described in the “Using Dependency Injection for Concrete Types” section.                                                                                                                                                                                         |
| AddTransient<service>(factoryFunc)                                                            | This method is used to register a factory function that will be invoked to create an implementation object for every dependency on the service type, as described in the “Using a Factory Function” section.                                                                                                                                                         |
| AddScoped<service, implType>()  AddScoped<service>()  AddScoped<service>(factoryFunc)         | These methods tell the service provider to reuse instances of the implementation type so that all service requests made by components associated with a common scope, which is usually a single HTTP request, share the same object. These methods follow the same pattern as the corresponding  AddTransientmethods. See the “Using the Scoped Life Cycle” section. |
| AddSingleton<service, implType>()  AddSingleton<service>()  AddSingleton<service(factoryFunc) | These methods tell the service provider to create a new instance of the implementation type for the first service request and then reuse it for every subsequent service request. See the “Using the Singleton Life Cycle” section.                                                                                                                                  |
| AddSingleton<service>(instance)                                                               | This method provides the service provider with an object that should be used to service all service requests. The service provider will not create any new objects.                                                                                                                                                                                                  |                                                                                                                                                                                                |

## Razor
### View location Expender
Razor uses view location expanders to build up a list of locations that should be searched for a view. View location expanders implement the IViewLocationExpander interface


