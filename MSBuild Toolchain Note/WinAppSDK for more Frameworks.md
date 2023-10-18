# Windows App SDK for more Frameworks

## Using Windows App SDK with .NET Built-in WinRT Interop

> [!NOTE]
> - Apply: Windows App SDK 1.0-pre1 ~ 1.8-exp1
> - Target:
>     - .NET Framework 4.5 +
>     - .NET Core 3.0 ~ 3.1
> - Dependency:
>     - Windows Runtime APIs Metadata (e.g. Microsoft.Windows.SDK.Contracts)
>     - Microsoft.Web.WebView2 (Windows App SDK 1.6-exp2 +)

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
```
