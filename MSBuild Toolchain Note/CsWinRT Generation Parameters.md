# C#/WinRT Generation Parameters


## Windows.UI.Xaml Projection

- Required: Microsoft.Windows.CsWinRT
- Dependency: Microsoft.Windows.SDK.NET.Ref

> [!WARNING]
> C#/WinRT doesn't support .NET mappings of WUX types.

> [!TIP]
> - UAC_VERSION_* is determined by the target version of Windows.Foundation.UniversalApiContract. E.g., If the target Windows version is 22621, please define `UAC_VERSION_15`.
> - Disable the warning 0436, due to Windows.UI.Color unable to be excluded.

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
  <DefineConstants>$(DefineConstants);MANUAL_IUNKNOWN,UAC_VERSION_*</DefineConstants>
  <NoWarn>$(NoWarn);0436</NoWarn>
</PropertyGroup>
```
