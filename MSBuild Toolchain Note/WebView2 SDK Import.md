# Microsoft Edge WebView2 SDK Import

## Import WebView2 WinRT instead of WebView2 .NET in .NET Framework Project

> [!NOTE]
> Apply : Microsoft.Web.WebView2 1.0.1018-pre +

> [!TIP]
> - Microsoft.Web.WebView2 1.0.955-pre ~ 1.0.1010-pre has had WebView2 WinRT. Microsoft.Web.WebView2.Core.winmd will be imported when TargetPlatformIdentifier is UAP. Before 1.0.1018-pre, there is no WebView2UseWinRT Property in WebView2 SDK.
> - From 1.0.2646-pre, set WebView2EnableCsWinRTProjection to false, while using Windows App SDK.
> - From 1.0.2783-pre, if you want to use WebView Win32 when WebView2UseWinRT is true , set WebView2NeverCopyLoaderDllToOutputDirectory to false. Before 1.0.2783-pre, you need import WebView2Loader.dll manually.

```XML
<PropertyGroup>
  <WebView2UseWinRT>true</WebView2UseWinRT>
  <WebView2EnableCsWinRTProjection>false</WebView2EnableCsWinRTProjection>
  <WebView2NeverCopyLoaderDllToOutputDirectory>false</WebView2NeverCopyLoaderDllToOutputDirectory>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="Microsoft.Web.WebView2" ExcludeAssets="compile;runtime" />
</ItemGroup>
```

## Import both WebView2 Win32 and WebView2 WinRT in MSVC++ Project

> [!NOTE]
> Apply : Microsoft.Web.WebView2 1.0.1018-pre +

> [!TIP]
> - Microsoft.Web.WebView2 1.0.955-pre ~ 1.0.1010-pre has had WebView2 WinRT. Microsoft.Web.WebView2.Core.winmd will be imported when TargetPlatformIdentifier is UAP. Before 1.0.1018-pre, there is no WebView2UseWinRT Property in WebView2 SDK.
> - If you want link WebView2Loader.dll statically, set WebView2LoaderPreference to Static.

```XML
<PropertyGroup>
  <WebView2UseWinRT>true</WebView2UseWinRT>
  <WebView2LoaderPreference>Dynamic</WebView2LoaderPreference>
</PropertyGroup>
```
