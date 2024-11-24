# XAML Window Internal API

## runtimeclass Windows.UI.Xaml.Window

> [!NOTE]
> - Implementation:
>     1. DirectUI::Window $\leftarrow$ DirectUI::WindowGenerated $\leftarrow$ DirectUI::DependencyObject
>     2. DirectUI::WindowFactory $\leftarrow$ ctl::AbstractActivationFactory
> - Library: Windows.UI.Xaml.dll

> [!TIP]
> DirectUI.Window is an implementation class with a GUID which can be querid in Windows.UI.Xaml.Window.QueryInterface.

```MIDL
namespace Windows.UI.Xaml
{
    [static(Windows.UI.Xaml.IWindowStatics, NTDDI_WIN8)]
    [version(NTDDI_WIN8)]
    runtimeclass Window : Windows.UI.Xaml.DependencyObject
    {
        [default] interface Windows.UI.Xaml.IWindow;
        [version(NTDDI_WIN10)] interface Windows.UI.Xaml.IWindowPrivate;
        [version(NTDDI_WIN10)] interface Windows.UI.Xaml.IWindow2;
        [version(NTDDI_WIN10_CO)] interface Windows.UI.Composition.ICompositionSupportsSystemBackdrop;
        [version(NTDDI_WIN10_RS2)] interface Windows.UI.Xaml.IWindow3;
        [version(NTDDI_WIN10_19H1)] interface Windows.UI.Xaml.IWindow4;
    }
}

namespace DirectUI
{
    [exclusiveto(Windows.UI.Xaml.Window)]
    [uuid(A14C9DB8-673D-4722-91D2-4A849FBFE3BF)]
    [version(NTDDI_WIN10)]
    interface Window{ }
}
```


### interface Windows.UI.Xaml.IWindowPrivate

> [!NOTE]
> The documented name of this interface is [Windows.UI.Xaml.IXamlSourceTransparency](https://learn.microsoft.com/windows/apps/api-reference/interface-members/ixamlsourcetransparency-isbackgroundtransparent)

> [!TIP]
> SetUseMonitorBoundsForPopupNudging has been implemented since Windows Gallium or Germanium, but Gallium didn't enter release branches, so attribute this to NTDDI_WIN11_GE.

```MIDL
namespace Windows.UI.Xaml
{
    [exclusiveto(Windows.UI.Xaml.Window)]
    [uuid(06636C29-5A17-458D-8EA2-2422D997A922)]
    [version(NTDDI_WIN10)]
    interface IWindowPrivate : IInspectable
    {
        Boolean BackgroundTransparent{ get; set; };
        void Show();
        void Hide();
        void MoveWindow(Int32 x, Int32 y, Int32 width, Int32 height);
        void SetAtlasSizeHint(UInt32 width, UInt32 height);
        [version(NTDDI_WIN10_RS2)] void ReleaseGraphicsDeviceOnSuspend(Boolean enable);
        [version(NTDDI_WIN10_RS3)] void SetAtlasRequestCallback(Windows.UI.Xaml.IAtlasRequestCallback callback);
        [version(NTDDI_WIN10_RS3)] void SetSynchronizationInfo(UInt64/*HANDLE*/ hDCompSyncObject, UInt64/*HWND*/ hCommitResizeWindow);
        [version(NTDDI_WIN10_RS5)] Windows.Foundation.Rect GetWindowContentBoundsForElement(Windows.UI.Xaml.DependencyObject element);
        [version(NTDDI_WIN10_RS5)] Windows.Foundation.Rect GetWindowContentLayoutBoundsForElement(Windows.UI.Xaml.DependencyObject element);
        [version(NTDDI_WIN11_GE)] void SetUseMonitorBoundsForPopupNudging(Boolean useMonitorBounds);
    }
}
```


#### interface Windows.UI.Xaml.IAtlasRequestCallback

> [!TIP]
> IAtlasRequestCallback is defined in Windows.UI.Xaml.dll without implementation, but AtlasRequest is implemented in DirectUI::Window.

```
namespace Windows.UI.Xaml
{
    [version(NTDDI_WIN10_RS3)]
    interface IAtlasRequestCallback : IInspectable
    {
        Boolean AtlasRequest(UInt32 width, UInt32 height, Windows.Graphics.DirectX.DirectXPixelFormat pixelFormat);
    }
}
```
