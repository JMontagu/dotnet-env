# dotenv.net

[![CircleCI](https://circleci.com/gh/bolorundurowb/dotenv.net.svg?style=svg)](https://circleci.com/gh/bolorundurowb/dotenv.net) [![NuGet Badge](https://buildstats.info/nuget/dotenv.net)](https://www.nuget.org/packages/dotenv.net) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) [![Book session on Codementor](https://cdn.codementor.io/badges/book_session_github.svg)](https://www.codementor.io/bolorundurowb?utm_source=github&utm_medium=button&utm_term=bolorundurowb&utm_campaign=github)

dotenv.net is a zero-dependency module that loads environment variables from a .env environment variable file into `System.Environment`. Please feel free to create issues with feature requests and raise bugs there too.

## Contributors

Big ups to those who have contributed to this library. :clap:

[@bolorundurowb](https://github.com/bolorundurowb) [@joliveros](https://github.com/joliveros) [@vizeke](https://github.com/vizeke) [@merqlove](https://github.com/merqlove) [@tracker1](https://github.com/tracker1) [@NaturalWill](https://github.com/NaturalWill)

## Usage

### Conventional

First install the library as a dependency in your application from nuget

```
Install-Package dotenv.net
```

or

```
dotnet add package dotenv.net
```

or for paket

```
paket add dotenv.net
```

Create a file with no filename and an extension of `.env`.

A sample `.env` file would look like this:

```text
DB_HOST=localhost
DB_USER=root
DB_PASS=s1mpl3
```

in the `Startup.cs` file or as early as possible in your code add the following:

```csharp
using dotenv.net;


...


DotEnv.Config();
```

the values saved in your `.env` file would be avaibale in your application and can be accessed via

```csharp
Environment.GetEnvironmentVariable("DB_HOST"); // would output 'localhost'
```

## Using with DI (`IServiceCollection`)

If using with ASP.NET Core or any other system that uses `IServiceCollection` for its dependency injection, in the `Startup.cs` file

```csharp
using dotenv.net.DependencyInjection.Extensions;

...

public void ConfigureServices(IServiceCollection services)
{
    ...

    // configure dotenv
    services.AddEnv(builder => {
        builder
        .AddEnvFile("/custom/path/to/your/env/vars")
        .AddThrowOnError(false)
        .AddEncoding(Encoding.ASCII);
    });
}
```

With this, your application would have the env file variables imported.

### Options

#### ThrowError

Default: `true`

You can specify if you want the library to error out if any issue arises or fail silently.

```csharp
DotEnv.Config(false); //fails silently
```

#### Path

Default: `.env`

You can specify a custom path if your file containing environment variables is
named or located differently.

```csharp
DotEnv.Config(true, "/custom/path/to/your/env/vars");
```

#### Encoding

Default: `Encoding.Default`

You may specify the encoding of your file containing environment variables
using this option.

```csharp
DotEnv.Config(true, ".env", Encoding.Unicode);
```
