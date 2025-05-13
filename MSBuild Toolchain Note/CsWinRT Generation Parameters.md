# C#/WinRT Generation Parameters


## Windows.UI.Xaml Projection

> [!NOTE]
> - Required: Microsoft.Windows.CsWinRT 2.1.0-prerelease.240602.1 and before
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
