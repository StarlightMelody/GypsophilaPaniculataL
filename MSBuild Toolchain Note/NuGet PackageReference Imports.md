# NuGet PackageReference Imports

## Enable PackageReference for Native MSVC Project

> [!NOTE]
> - Apply: MSBuild 16+
> - Required: Desktop development with C++ workload

```XML
<ItemGroup Label="ProjectConfigurations">
  ...
  <ProjectCapability Include="PackageReferences" />
</ItemGroup>
<PropertyGroup Label="Configuration">
  ...
  <TargetFramework>native</TargetFramework>
  <TargetFrameworkIdentifier>$([MSBuild]::GetTargetFrameworkIdentifier('$(TargetFramework)'))</TargetFrameworkIdentifier>
  <TargetFrameworkVersion>v$([MSBuild]::GetTargetFrameworkVersion('$(TargetFramework)', 2))</TargetFrameworkVersion>
  <TargetPlatformIdentifier>$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)'))</TargetPlatformIdentifier>
  <TargetPlatformVersion>$(WindowsTargetPlatformVersion)</TargetPlatformVersion>
  <TargetFrameworkIdentifier Condition="'$(DesignTimeBuild)' == 'true'">.NETCore</TargetFrameworkIdentifier>
  <TargetFrameworkVersion Condition="'$(DesignTimeBuild)' == 'true'">v5.0</TargetFrameworkVersion>
  <!-- TBD... XAML Designer for UWP or Islands 
    <TargetPlatformIdentifier Condition="'$(DesignTimeBuild)' == 'true' or '$(AppContainerApplication)' == 'true'">UAP</TargetPlatformIdentifier>
  -->
</PropertyGroup>
```
