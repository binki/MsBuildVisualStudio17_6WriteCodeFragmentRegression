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
