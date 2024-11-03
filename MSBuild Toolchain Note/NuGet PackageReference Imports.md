# NuGet PackageReference Imports

## Enable PackageReference for Native MSVC Project

> [!NOTE]
> Apply: MSBuild 16+

```XML
<ItemGroup Label="ProjectConfigurations">
  ...
  <ProjectCapability Include="PackageReferences" />
</ItemGroup>
<PropertyGroup Label="Globals">
  ...
  <EnableManagedPackageReferenceSupport>true</EnableManagedPackageReferenceSupport>
  <TargetFrameworkIdentifier>native</TargetFrameworkIdentifier>
  <TargetFrameworkVersion>v0.0</TargetFrameworkVersion>
  <TargetPlatformIdentifier>windows</TargetPlatformIdentifier>
  <TargetPlatformVersion>$(WindowsTargetPlatformVersion)</TargetPlatformVersion>
</PropertyGroup>
```
