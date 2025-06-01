# WinRT XAML Application Internal API

## runtimeclass Windows.UI.Xaml.Application

### interface Windows.UI.Xaml.IFrameworkApplicationPrivate
```MIDL
namespace Windows.UI.Xaml
{
    [exclusiveto(Windows.UI.Xaml.Application)]
    [uuid(B3AB45D8-6A4E-4E76-A00D-32D4643A9F1A)]
    [version(NTDDI_WIN10_RS2)]
    interface IFrameworkApplicationPrivate : IInspectable
    {
        void StartOnCurrentThread(Windows.UI.Xaml.ApplicationInitializationCallback callback);
        Windows.UI.Xaml.Hosting.XamlIsland CreateIsland();
        [version(NTDDI_WIN10_19H1)] Windows.UI.Xaml.Hosting.XamlIsland CreateIslandWithAppWindow(Windows.UI.WindowManagement.AppWindow appWindow);
        [version(NTDDI_WIN10_19H1)] Windows.UI.Xaml.Hosting.XamlIsland CreateIslandWithContentBridge(IInspectable owner, IInspectable/*Windows.UI.Core.(Private.)DesktopWindowContentBridge*/ contentBridge);
        [version(NTDDI_WIN10_RS3)] void RemoveIsland(Windows.UI.Xaml.Hosting.XamlIsland island);
        [version(NTDDI_WIN10_RS4)] void SetSynchronizationWindow(UInt64/*HWND*/ commitResizeWindow);
    }
}
```
