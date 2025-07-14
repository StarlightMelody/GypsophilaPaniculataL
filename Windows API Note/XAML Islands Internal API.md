# XAML Islands Internal API

## runtimeclass Windows.UI.Xaml.Hosting.XamlIsland
> [!NOTE]
> - Implementation:
>     1. DirectUI::XamlIsland $\leftarrow$ DirectUI::XamlIslandGenerated $\leftarrow$ DirectUI::Panel
>     2. DirectUI::XamlIslandFactory $\leftarrow$ ctl::BetterCoreObjectActivationFactory
> - Library: Windows.UI.Xaml.dll

> [!TIP]
> DirectUI.XamlIslandGenerated is an implementation class with a GUID which can be querid in QueryInterface.

```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [marshaling_behavior(agile)]
    [static(Windows.UI.Xaml.Hosting.IXamlIslandStatics, NTDDI_WIN10_RS2)]
    [threading(both)]
    [version(NTDDI_WIN10_RS2)]
    runtimeclass XamlIsland : Windows.UI.Xaml.Controls.Panel
    {
        [default] interface Windows.UI.Xaml.Hosting.IXamlIsland;
    }
}
namespace DirectUI
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlIsland)]
    [uuid(412B49D7-B8B7-416A-B49B-57F9EDBEF991)]
    [version(NTDDI_WIN10_RS2)]
    interface XamlIslandGenerated : Windows.UI.Xaml.Hosting.IXamlIsland{ }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlIsland
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlIsland)]
    [uuid(36A01E0A-D6AA-4779-8256-25FE90B7679C)]
    [version(NTDDI_WIN10_RS2)]
    interface IXamlIsland : IInspectable
    {
        [version(NTDDI_WIN10_RS3), deprecated("", remove, NTDDI_WIN10_19H1)] Windows.UI.Composition.CompositionIsland CompositionIsland{ get; };
        [version(NTDDI_WIN10_19H1)] Windows.UI.UIContentRoot AppContent{ get; };
        Windows.UI.Xaml.UIElement Content{ get; set; };
        [deprecated("", remove, NTDDI_WIN10_RS3)] Windows.Foundation.Size Size{ get; set; };
        [deprecated("", remove, NTDDI_WIN10_RS3)] Windows.UI.Input.IPointerPointTransform PointerPointTransform{ get; set; };
        [deprecated("", remove, NTDDI_WIN10_RS3)] Windows.UI.Composition.Visual GetSharedVisual(Windows.UI.Composition.Compositor comp);
        [deprecated("", remove, NTDDI_WIN10_RS3)] void InjectPointerCaptureLost(Windows.UI.Core.PointerEventArgs args);
        [deprecated("", remove, NTDDI_WIN10_RS3)] void InjectPointerEntered(Windows.UI.Core.PointerEventArgs args);
        [deprecated("", remove, NTDDI_WIN10_RS3)] void InjectPointerExited(Windows.UI.Core.PointerEventArgs args);
        [deprecated("", remove, NTDDI_WIN10_RS3)] void InjectPointerMoved(Windows.UI.Core.PointerEventArgs args);
        [deprecated("", remove, NTDDI_WIN10_RS3)] void InjectPointerPressed(Windows.UI.Core.PointerEventArgs args);
        [deprecated("", remove, NTDDI_WIN10_RS3)] void InjectPointerReleased(Windows.UI.Core.PointerEventArgs args);
        [version(NTDDI_WIN10_RS5)] Windows.UI.Xaml.Hosting.FocusController FocusController{ get; };
        [version(NTDDI_WIN10_RS5)] Windows.UI.CustomMaterialProperties MaterialProperties{ get; set; };
        [version(NTDDI_WIN10_RS4)] void SetScreenOffsetOverride(Windows.Foundation.Point offsetOnScreen);
        [version(NTDDI_WIN10_RS4)] void SetFocus();
    }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlIslandStatics
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlIsland)]
    [uuid(3EAD2336-B073-456F-BCAF-82587EB63487)]
    [version(NTDDI_WIN10_RS2)]
    interface IXamlIslandStatics : IInspectable
    {
        [deprecated("", remove, NTDDI_WIN10_RS3)] Windows.UI.Xaml.DependencyProperty SizeProperty{ get; };
        [version(NTDDI_WIN10_RS5)] Windows.UI.Xaml.Hosting.XamlIsland GetIslandFromElement(Windows.UI.Xaml.DependencyObject element);
    }
}
```
