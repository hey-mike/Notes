# Dotnet notes

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

5. Run the app

```bash
dotnet run
```

or 
```
ASPNETCORE_ENVIRONMENT=Development dotnet run
```