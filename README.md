# Visual Studio 17.6.x WriteCodeFragment Regression

When using the `WriteCodeFragment` task in Visual Studio 17.6.0 (tested) and 17.6.2 (tested) (it is assumed that 17.6.1 is affected as well as unreleased future versions) with an `OutputFile` parameter referring to a file which starts with a dot (`.`), an error is encountered.

Consider this excerpt from `.csproj` which would be in a `Target`:

```xml
<ItemGroup>
  <TestAttribute Include="System.Reflection.AssemblyTitleAttribute">
    <_Parameter1>1.2.3</_Parameter1>
  </TestAttribute>
</ItemGroup>
<WriteCodeFragment AssemblyAttributes="@(TestAttribute)" Language="C#" OutputFile=".test.cs" />
```

The above fails with this error:

```
C:\Users\binki\source\repos\MsBuildVisualStudio17_6WriteCodeFragmentRegression\proj.csproj(11,5): error MSB3713: The file ".test.cs" could not be created. Path cannot be the empty string or all whitespace.
```

## Tests

### 17.5.5

Bug absent. This error is not reproducible in visualstudio-17.5.5 (tested):

```
MSBuild version 17.5.1+f6fdcf537 for .NET Framework
17.5.1.16304
```

```
Microsoft Visual Studio Professional 2022
Version 17.5.5
VisualStudio.17.Release/17.5.5+33627.172
Microsoft .NET Framework
Version 4.8.09032

Installed Version: Professional

ASP.NET and Web Tools   17.5.320.55692
ASP.NET and Web Tools

Azure App Service Tools v3.0.0   17.5.320.55692
Azure App Service Tools v3.0.0

C# Tools   4.5.2-3.23171.7+d17f741546fad2786cbd6394d08619544e53a36d
C# components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Common Azure Tools   1.10
Provides common services for use by Azure Mobile Services and Microsoft Azure Tools.

Microsoft JVM Debugger   1.0
Provides support for connecting the Visual Studio debugger to JDWP compatible Java Virtual Machines

NuGet Package Manager   6.5.0
NuGet Package Manager in Visual Studio. For more information about NuGet, visit https://docs.nuget.org/

Razor (ASP.NET Core)   17.5.2.2316603+9f1b6856460af1e592d387ebef416eadddac453f
Provides languages services for ASP.NET Core Razor.

SQL Server Data Tools   17.2.40120.0
Microsoft SQL Server Data Tools

TypeScript Tools   17.0.20105.2003
TypeScript Tools for Microsoft Visual Studio

Visual Basic Tools   4.5.2-3.23171.7+d17f741546fad2786cbd6394d08619544e53a36d
Visual Basic components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Visual F# Tools   17.5.0-beta.23053.5+794b7c259d9646a7eb685dad865aa27da7940a21
Microsoft Visual F# Tools
```

### 17.6.0

Bug present.

```
MSBuild version 17.6.3+07e294721 for .NET Framework
17.6.3.22601
```

```
Microsoft Visual Studio Community 2022
Version 17.6.0
VisualStudio.17.Release/17.6.0+33712.159
Microsoft .NET Framework
Version 4.8.09032

Installed Version: Community

Visual C++ 2022   00482-90000-00000-AA915
Microsoft Visual C++ 2022

ASP.NET and Web Tools   17.6.326.62524
ASP.NET and Web Tools

Azure App Service Tools v3.0.0   17.6.326.62524
Azure App Service Tools v3.0.0

C# Tools   4.6.0-3.23259.8+c3cc1d0ceeab1a65da0217e403851a1e8a30086a
C# components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Common Azure Tools   1.10
Provides common services for use by Azure Mobile Services and Microsoft Azure Tools.

Microsoft JVM Debugger   1.0
Provides support for connecting the Visual Studio debugger to JDWP compatible Java Virtual Machines

NuGet Package Manager   6.6.0
NuGet Package Manager in Visual Studio. For more information about NuGet, visit https://docs.nuget.org/

Razor (ASP.NET Core)   17.6.0.2326105+37f2727000f6a964584cafb86e69cf0b39baecb7
Provides languages services for ASP.NET Core Razor.

SQL Server Data Tools   17.6.13.0
Microsoft SQL Server Data Tools

SQL Server Reporting Services   16.0.20286.0
Microsoft SQL Server Reporting Services Designers 
Version 16.0.20286.0

Syntax Visualizer   1.0
An extension for visualizing Roslyn SyntaxTrees.

TypeScrip   17.0.20329.2001
TypeScript Tools for Microsoft Visual Studio

Visual Basic Tools   4.6.0-3.23259.8+c3cc1d0ceeab1a65da0217e403851a1e8a30086a
Visual Basic components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Visual F# Tools   17.6.0-beta.23174.5+0207bea1afae48d9351ac26fb51afc8260de0a97
Microsoft Visual F# Tools

Visual Studio IntelliCode   2.2
AI-assisted development for Visual Studio.
```

### 17.6.2

Bug present.

```
MSBuild version 17.6.3+07e294721 for .NET Framework
17.6.3.22601
```

```
Microsoft Visual Studio Professional 2022
Version 17.6.2
VisualStudio.17.Release/17.6.2+33723.286
Microsoft .NET Framework
Version 4.8.09032

Installed Version: Professional

ASP.NET and Web Tools   17.6.326.62524
ASP.NET and Web Tools

Azure App Service Tools v3.0.0   17.6.326.62524
Azure App Service Tools v3.0.0

C# Tools   4.6.0-3.23259.8+c3cc1d0ceeab1a65da0217e403851a1e8a30086a
C# components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Common Azure Tools   1.10
Provides common services for use by Azure Mobile Services and Microsoft Azure Tools.

Microsoft JVM Debugger   1.0
Provides support for connecting the Visual Studio debugger to JDWP compatible Java Virtual Machines

NuGet Package Manager   6.6.0
NuGet Package Manager in Visual Studio. For more information about NuGet, visit https://docs.nuget.org/

Razor (ASP.NET Core)   17.6.0.2326105+37f2727000f6a964584cafb86e69cf0b39baecb7
Provides languages services for ASP.NET Core Razor.

SQL Server Data Tools   17.6.13.0
Microsoft SQL Server Data Tools

SQL Server Reporting Services   16.0.20309.0
Microsoft SQL Server Reporting Services Designers 
Version 16.0.20309.0

TypeScript Tools   17.0.20329.2001
TypeScript Tools for Microsoft Visual Studio

Visual Basic Tools   4.6.0-3.23259.8+c3cc1d0ceeab1a65da0217e403851a1e8a30086a
Visual Basic components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Visual F# Tools   17.6.0-beta.23174.5+0207bea1afae48d9351ac26fb51afc8260de0a97
Microsoft Visual F# Tools

Visual Studio IntelliCode   2.2
AI-assisted development for Visual Studio.
````

## Status

This has been reported to Microsoft as [Visual Studio feedback item 10378111](https://developercommunity.visualstudio.com/t/-/10378111).
