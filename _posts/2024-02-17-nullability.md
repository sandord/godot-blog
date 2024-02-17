---
title: Working with nullability
date: 2024-02-17
---
## Introduction to nullable reference types

> TLDR; nullable references help you write more concise and less buggy code that is easier to understand.

Since C# introduced [nullable references](https://learn.microsoft.com/en-us/dotnet/csharp/nullable-references) (also called NRTs) back in version 8, it has been possible to tell the C# compiler which reference types are supposed to be nullable and which are not by changing the default for reference types to be not-null and using the `?` suffix on type names to declare types as nullable.

```csharp
// Declare some nullable strings.
string? name1a = null;
string? name1b = "";

// Declare some non-nullable strings.
string name2a = null; // Won't compile
string name2b = "";
```

Using nullable types provides the compiler with additional information which it can use to detect potential issues with your code. Like in the example above, the compiler won't allow you to assign `null` to a non-nullable variable. Without nullable types, doing so would've resulted in a runtime exception but only when the code path was actually hit.

The introduction of nullable types can be seen as a mitigation for the [Billion Dollar Mistake](https://www.infoq.com/presentations/Null-References-The-Billion-Dollar-Mistake-Tony-Hoare).

A lot of software bugs can be attributed to NRTs where a reference is `null` in a situation where it isn't expected to be.

The nullable references feature is enabled by adding the `Nullable` node to a property group in your `.csproj` file:

```xml
<Project>
    <PropertyGroup>
        <Nullable>enable</Nullable>
    </PropertyGroup>
</Project>
```

The nullable references feature is enabled by default for most new project templates though so it's probably enabled already in your project if you created it not too long ago.

## 