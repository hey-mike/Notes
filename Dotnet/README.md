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
ASPNETCORE_ENVIRONMENT=Development dotnet run
```


