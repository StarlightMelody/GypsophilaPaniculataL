# XAML Application Internal API

## runtimeclass Windows.UI.Xaml.Application

> [!NOTE]
> - Implementation(Win8):
>     - Windows 8.X:
>         1. DirectUI::Application $\leftarrow$ DirectUI::ApplicationGenerated $\leftarrow$ ctl::WeakReferenceSource
>         2. DirectUI::ApplicationFactory $\leftarrow$ ctl::AggregableActivationFactory
>     - Windows 10+:
>         1. DirectUI::FrameworkApplication $\leftarrow$ DirectUI::FrameworkApplicationGenerated $\leftarrow$ ctl::WeakReferenceSource
>         2. DirectUI::FrameworkApplicationFactory $\leftarrow$ ctl::AggregableActivationFactory
> - Library: Windows.UI.Xaml.dll

```C#
namespace Windows.UI.Xaml
{
    [version(NTDDI_WIN8)]
    [marshaling_behavior(agile)]
    [threading(both)]
    [composable(Windows.UI.Xaml.IApplicationFactory, public, NTDDI_WIN8)]
    [static(Windows.UI.Xaml.IApplicationStatics, NTDDI_WIN8)]
    [static(Windows.UI.Xaml.IFrameworkApplicationStaticsPrivate, NTDDI_WIN10)]
    runtimeclass Application : DirectUI.FrameworkApplicationGenerated
    {
        [default] interface Windows.UI.Xaml.IApplication;
        [overridable] interface Windows.UI.Xaml.IApplicationOverrides;
        [version(NTDDI_WIN10_RS2)] interface Windows.UI.Xaml.IFrameworkApplicationPrivate;
        [version(NTDDI_WIN10_RS1)] interface Windows.UI.Xaml.IApplication2;
        [version(NTDDI_WIN10_RS1)] [overridable] interface Windows.UI.Xaml.IApplicationOverrides2;
        [version(NTDDI_WIN10_RS2)] interface Windows.UI.Xaml.IApplication3;
    };
}

namespace DirectUI
{
    [exclusiveto(Windows.UI.Xaml.Application)]
    [uuid("A3DD6C47-5F62-4534-9EEF-FDCDBB120779")]
    [version(NTDDI_WIN10)]
    interface FrameworkApplicationGenerated : IInspectable{ };
}
```

### interface Windows.UI.Xaml.IFrameworkApplicationPrivate

```C#
namespace Windows.UI.Xaml
{
    [exclusiveto(Windows.UI.Xaml.Application)]
    [uuid("B3AB45D8-6A4E-4E76-A00D-32D4643A9F1A")]
    [version(NTDDI_WIN10_RS2)]
    interface IFrameworkApplicationPrivate : IInspectable
    {
        void StartOnCurrentThread(Windows.UI.Xaml.ApplicationInitializationCallback callback);
        Windows.UI.Xaml.Hosting.XamlIsland CreateIsland();
        [version(NTDDI_WIN10_19H1)] Windows.UI.Xaml.Hosting.XamlIsland CreateIslandWithAppWindow(Windows.UI.WindowManagement.AppWindow appWindow);
        [version(NTDDI_WIN10_19H1)] Windows.UI.Xaml.Hosting.XamlIsland CreateIslandWithContentBridge(IInspectable owner, IInspectable/*Windows.UI.Core.(Private.)DesktopWindowContentBridge*/ contentBridge);
        [version(NTDDI_WIN10_RS3)] void RemoveIsland(Windows.UI.Xaml.Hosting.XamlIsland island);
        [version(NTDDI_WIN10_RS4)] void SetSynchronizationWindow(UInt64/*HWND*/ commitResizeWindow);
    };
}
```

### interface Windows.UI.Xaml.IFrameworkApplicationStaticsPrivate

```C#
namespace Windows.UI.Xaml
{
    [exclusiveto(Windows.UI.Xaml.Application)]
    [uuid("C45F3F8C-61E6-4F9A-BE88-FE4FE6E64F5F")]
    [version(NTDDI_WIN10)]
    interface IFrameworkApplicationStaticsPrivate : IInspectable
    {
        void StartInCoreWindowHostingMode(Windows.UI.Xaml.WindowCreationParameters initialWindowConfiguration, Windows.UI.Xaml.ApplicationInitializationCallback callback);
        [version(NTDDI_WIN10_RS4)] void EnableFailFastOnStowedException();
    };
}
```

#### struct Windows.UI.Xaml.WindowCreationParameters

```C#
namespace Windows.UI.Xaml
{
    [version(NTDDI_WIN10)]
    struct WindowCreationParameters
    {
        Int32 Left;
        Int32 Top;
        Int32 Width;
        Int32 Height;
        Boolean TransparentBackground;
        [version(NTDDI_WIN10_RS2)] Boolean IsCoreNavigationClient;
    };
}
```
