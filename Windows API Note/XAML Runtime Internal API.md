# XAML Runtime Internal API

## runtimeclass Windows.UI.Xaml.Hosting.XamlRuntime

> [!NOTE]
> - Implementation: DirectUI::XamlRuntimeFactory $\leftarrow$ ctl::AbstractActivationFactory
> - Library: Windows.UI.Xaml.dll

```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [static(Windows.UI.Xaml.Hosting.IXamlRuntimeStatics, NTDDI_WINBLUE)]
    [version(NTDDI_WINBLUE)]
    runtimeclass XamlRuntime{ }
}
```


### interface Windows.UI.Xaml.Hosting.IXamlRuntimeStatics

```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlRuntime)]
    [uuid(C805B0C0-6210-4E4F-B76A-E894E8B1A4AD)]
    [version(NTDDI_WINBLUE)]
    interface IXamlRuntimeStatics : IInspectable
    {
        Boolean EnableImmersiveColors{ get; set; };
        Boolean EnableWebView{ get; set; };
        void SetSite(Windows.UI.Xaml.Hosting.IXamlRuntimeSite site);
    }
}
```


#### interface Windows.UI.Xaml.Hosting.IXamlRuntimeSite

> [!NOTE]
> Its GUID is found in ViewDefinitionBase::_EnsureSiteInitialized where in the DLLs(e.g. Windows.UI.CredDialogController.dll) which uses Windows.Internal.UI.XAMLHost.XAMLHostWindow.

> [!TIP]
> IXamlRuntimeSite is defined in Windows.UI.Xaml.dll without implementation.

```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [uuid(1C35E215-859E-41A3-922B-303B8699A29D)]
    [version(NTDDI_WINBLUE)]
    interface IXamlRuntimeSite : IInspectable{ }
}
```
