# Windows App SDK for more Frameworks

## Built-in WinRT Interop for .NET

```XML
<PropertyGroup>
  <WindowsAppSDKVerifyWinrtRuntimeVersion>false</WindowsAppSDKVerifyWinrtRuntimeVersion>
</PropertyGroup>
<ItemGroup>
  <Reference Include="$(MicrosoftWindowsAppSDKPackageDir)\lib\uap10.0\*.winmd" />
  <Reference Include="$(MicrosoftWindowsAppSDKPackageDir)\lib\$(Ixp-UAPTargetVersion)\*.winmd" />
</ItemGroup>
<Target Name="RemoveCSWinRTFlag" BeforeTargets="BeforeBuild">
  <PropertyGroup>
    <_UsingCSWinRT>false</_UsingCSWinRT>
  </PropertyGroup>
  <ItemGroup>
    <XamlFeatureControlFlags Remove="UsingCSWinRT" />
  </ItemGroup>
</Target>
```
