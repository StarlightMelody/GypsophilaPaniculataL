# Windows App SDK for more Frameworks

## Using Windows App SDK by .NET Built-in WinRT Interop

> [!NOTE]
> - Apply: Windows App SDK 1.0-pre1 ~ 1.8-exp1
> - Target:
>     - .NET Framework 4.5 +
>     - .NET Core 3.0 ~ 3.1
> - Dependency: Microsoft.Web.WebView2 (Windows App SDK 1.6-exp2 ~ 1.8-exp1)

> [!IMPORTANT]
> From 1.6-exp2, need [import WebView2 WinRT instead of WebView2 .NET in .NET Framework project](./WebView2%20SDK%20Import.md#import-webview2-winrt-instead-of-webview2-net-in-net-framework-project)

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
