# Unity Game Mod Development

## Cities : Skylines

> [!NOTE]
> - Apply: Cities : Skylines (Steam Version)

> [!TIP]
> If the game isn't installed by Steam, please alter `FrameworkPathOverride`.

```XML
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net35</TargetFramework>
    <Platforms>x64</Platforms>
    <EnableNETAnalyzers>true</EnableNETAnalyzers>
    <FrameworkPathOverride>$(registry:HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Steam App 255710@InstallLocation)\Cities_Data\Managed</FrameworkPathOverride>
    <NoStdLib>true</NoStdLib>
    <DisableImplicitFrameworkReferences>true</DisableImplicitFrameworkReferences>
    <AutomaticallyUseReferenceAssemblyPackages>false</AutomaticallyUseReferenceAssemblyPackages>
  </PropertyGroup>

  <ItemGroup Condition="Exists('$(FrameworkPathOverride)')">
    <Reference Include="$(FrameworkPathOverride)\*.dll" Pack="false" />
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="CitiesHarmony.API" Version="2.2.0" ExcludeAssets="runtime" PrivateAssets="all" />
  </ItemGroup>

</Project>
```
