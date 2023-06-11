# WinRT XAML for more Frameworks

> [!NOTE]
> - Target:
>     - .NET Framework 4.5 +
>     - .NET Core 3.0 ~ 3.1

## Common UWP project settings
```XML
<PropertyGroup>
  <WindowsAppContainer>true</WindowsAppContainer>
  <DefineConstants>$(DefineConstants);NETFX_CORE;WINDOWS_UWP</DefineConstants>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="Microsoft.Windows.SDK.Contracts" />
</ItemGroup>
```

## Xaml Compiler
```XML
<PropertyGroup>
  <DefaultXamlRuntime>UAP</DefaultXamlRuntime>
  <ImportFrameworkWinFXTargets>false</ImportFrameworkWinFXTargets>
  <_EnableWindowsDesktopGlobbing>true</_EnableWindowsDesktopGlobbing>
  <SDKIdentifier>Windows</SDKIdentifier>
  <SDKVersion>10.0</SDKVersion>
  <CustomAfterMicrosoftCSharpTargets>
    $(CustomAfterMicrosoftCSharpTargets);
    $(MSBuildExtensionsPath)\Microsoft\WindowsXaml\v$(VisualStudioVersion)\8.21\Microsoft.Windows.UI.Xaml.Common.targets;
    $(MSBuildExtensionsPath)\Microsoft\WindowsXaml\v$(VisualStudioVersion)\8.21\Microsoft.Windows.UI.Xaml.Cps.targets
  </CustomAfterMicrosoftCSharpTargets>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="Microsoft.Windows.SDK.CPP" />
</ItemGroup>
```

## Single-project AppX packaging
```XML
<PropertyGroup>
  <AppxPackage>true</AppxPackage>
  <DefaultLanguage>en</DefaultLanguage>
  <AppxGeneratePrisForPortableLibrariesEnabled>false</AppxGeneratePrisForPortableLibrariesEnabled>
</PropertyGroup>
<ItemGroup>
  <AppxManifest Include="Package.appxmanifest" SubType="Designer" />
  <ProjectCapability Include="Msix" />
  <PackageReference Include="Microsoft.Windows.SDK.BuildTools" />
</ItemGroup>
```

## Sample

### UWP on .NET Framework 4.8.1 or .NET Core 3.1
- ProjectName.csproj
```XML
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net481;netcoreapp3.1</TargetFramework>
    <TargetPlatformVersion>10.0.26100.0</TargetPlatformVersion>
    <TargetPlatformMinVersion>10.0.26100.0</TargetPlatformMinVersion>
    <Platforms>x64</Platforms>
    <CheckEolTargetFramework>false</CheckEolTargetFramework>
  </PropertyGroup>

  <!-- Common UWP project settings-->
  <PropertyGroup>
    <WindowsAppContainer>true</WindowsAppContainer>
    <DefineConstants>$(DefineConstants);NETFX_CORE;WINDOWS_UWP</DefineConstants>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.Windows.SDK.Contracts" Version="$([System.Version]::Parse('$(TargetPlatformVersion)').ToString(3)).*" />
  </ItemGroup>

  <!-- XAML Compiler -->
  <PropertyGroup>
    <DefaultXamlRuntime>UAP</DefaultXamlRuntime>
    <ImportFrameworkWinFXTargets>false</ImportFrameworkWinFXTargets>
    <_EnableWindowsDesktopGlobbing>true</_EnableWindowsDesktopGlobbing>
    <SDKIdentifier>Windows</SDKIdentifier>
    <SDKVersion>10.0</SDKVersion>
    <CustomAfterMicrosoftCSharpTargets>
      $(CustomAfterMicrosoftCSharpTargets);
      $(MSBuildExtensionsPath)\Microsoft\WindowsXaml\v$(VisualStudioVersion)\8.21\Microsoft.Windows.UI.Xaml.Common.targets;
      $(MSBuildExtensionsPath)\Microsoft\WindowsXaml\v$(VisualStudioVersion)\8.21\Microsoft.Windows.UI.Xaml.Cps.targets
    </CustomAfterMicrosoftCSharpTargets>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.Windows.SDK.CPP" Version="$([System.Version]::Parse('$(TargetPlatformVersion)').ToString(3)).*" />
  </ItemGroup>

  <!-- Single-project AppX packaging -->
  <PropertyGroup>
    <AppxPackage>true</AppxPackage>
    <DefaultLanguage>en</DefaultLanguage>
    <AppxGeneratePrisForPortableLibrariesEnabled>false</AppxGeneratePrisForPortableLibrariesEnabled>
  </PropertyGroup>
  <ItemGroup>
    <AppxManifest Include="Package.appxmanifest" SubType="Designer" />
    <ProjectCapability Include="Msix" />
    <PackageReference Include="Microsoft.Windows.SDK.BuildTools" Version="$([System.Version]::Parse('$(TargetPlatformVersion)').ToString(3)).*" />
  </ItemGroup>

</Project>
```

- LaunchSettings.json
```JSON
{
  "profiles": {
    "ProjectName": {
      "commandName": "MsixPackage"
    }
  }
}
```
