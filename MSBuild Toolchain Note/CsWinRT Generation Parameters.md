# C#/WinRT Generation Parameters


## Windows.UI.Xaml Projection

> [!NOTE]
> - Applies: Microsoft.Windows.CsWinRT 2.1.0-prerelease.240602.1 and before
> - Dependency: Microsoft.Windows.SDK.NET.Ref 10.0.X.35-preview and before
> - **The newer C#/WinRT has supported .NET mappings of WUX types offically.**

> [!WARNING]
> The legacy C#/WinRT doesn't support .NET mappings of WUX types.

> [!IMPORTANT]
> UAC_VERSION_* is determined by the target version of Windows.Foundation.UniversalApiContract.\
> E.g., If target Windows version is 22621, please define `UAC_VERSION_15`.

> [!TIP]
> Disable the warning 0436, due to Windows.UI.Color unable to be excluded.

```XML
<PropertyGroup>
  <CsWinRTIncludes>
    Windows.UI.IColors;
    Windows.UI.Colors;
    Windows.UI.IColorHelper;
    Windows.UI.ColorHelper;
    Windows.UI.Xaml;
    Windows.UI.Text
  </CsWinRTIncludes>
  <CsWinRTExcludes>
    Windows.UI.Color;
    Windows.UI.Text.FontStretch;
    Windows.UI.Text.FontStyle;
    Windows.UI.Text.FontWeight;
    Windows.UI.Text.UnderlineType;
    Windows.UI.Text.Core
  </CsWinRTExcludes>
  <DefineConstants>$(DefineConstants);UAC_VERSION_15</DefineConstants>
  <NoWarn>$(NoWarn);0436</NoWarn>
</PropertyGroup>
```


## Windows Runtime API Projection for .NET Standard

> [!NOTE]
> - Applies: Microsoft.Windows.CsWinRT 1.4.1
> - Required: WinRT APIs Metadata (e.g. Microsoft.Windows.SDK.Contracts)
> 1. - Target: .NET Standard 2.0
>    - Dependency: System.Memory 4.5.2 +
> 2. - Target: .NET Standard 2.1
>    - Dependency: System.Runtime.CompilerServices.Unsafe 4.5.0 +

> [!IMPORTANT]
> UAC_VERSION_* is determined by the target version of Windows.Foundation.UniversalApiContract.\
> E.g., If target Windows version is 22621, please define `UAC_VERSION_15`.

> [!TIP]
> - Don't use C#/WinRT embedded mode, because every projection class will be modified by `internal` access modifier.
> - Don't merge WinRT.Runtime and Microsoft.Windows.SDK.NET into one library, because Windows.Foundation.PropertyType is defined both in WinRT.Runtime and Microsoft.Windows.SDK.NET, whose access modifiers are different.

- WinRT.Runtime.csproj
```XML
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;netstandard2.1</TargetFrameworks>
    <LangVersion>9</LangVersion>
    <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
    <CsWinRTEnabled>false</CsWinRTEnabled>
  </PropertyGroup>
  <ItemGroup>
    <Compile Include="$(CsWinRTPath)\embedded\any\*.cs" Visible="false" />
    <Compile Include="$(CsWinRTPath)\embedded\netstandard2.0\*.cs" Visible="false" />
  </ItemGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.Windows.CsWinRT" />
    <PackageReference Condition="'$(TargetFramework)' == 'netstandard2.0'" Include="System.Memory" />
    <PackageReference Condition="'$(TargetFramework)' == 'netstandard2.1'" Include="System.Runtime.CompilerServices.Unsafe" />
  </ItemGroup>
</Project>
```

- Microsoft.Windows.SDK.NET.csproj
```XML
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0;netstandard2.1</TargetFramework>
    <LangVersion>9</LangVersion>
    <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
    <_EnableDefaultWindowsPlatform>false</_EnableDefaultWindowsPlatform>
    <CsWinRTIncludes>Windows</CsWinRTIncludes>
    <CsWinRTExcludes>;</CsWinRTExcludes>
    <DefineConstants>UAC_VERSION_15</DefineConstants>
    <WarningLevel>0</WarningLevel>
  </PropertyGroup>
  <ItemGroup>
    <ProjectReference Include="..\WinRT.Runtime\WinRT.Runtime.csproj" />
    <PackageReference Include="Microsoft.Windows.CsWinRT" />
    <PackageReference Include="Microsoft.Windows.SDK.Contracts" PrivateAssets="all" />
    <PackageReference Include="System.Runtime.InteropServices.WindowsRuntime" ExcludeAssets="all" PrivateAssets="all" />
    <PackageReference Include="System.Runtime.WindowsRuntime" ExcludeAssets="all" PrivateAssets="all" />
    <PackageReference Include="System.Runtime.WindowsRuntime.UI.Xaml" ExcludeAssets="all" PrivateAssets="all" />
  </ItemGroup>
</Project>
```
