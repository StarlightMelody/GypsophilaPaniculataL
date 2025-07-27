# Core Title Bar Internal API

## runtimeclass Windows.ApplicationModel.Core.CoreApplicationViewTitleBar

> [!NOTE]
> - Implementation: Windows::ApplicationModel::Core::CoreApplicationViewTitleBar -> Microsoft::WRL::RuntimeClass<Microsoft::WRL::RuntimeClassFlags<RuntimeClassType::WinRtClassicComMix>>
> - Library: twinapi.appcore.dll

```MIDL
namespace Windows.ApplicationModel.Core
{
    [marshaling_behavior(standard)]
    [version(NTDDI_WIN10)]
    runtimeclass CoreApplicationViewTitleBar
    {
        interface IUnknown;
        interface IInspectable;
        [default] interface Windows.ApplicationModel.Core.ICoreApplicationViewTitleBar;
        interface IWeakReferenceSource;
        interface ICoreApplicationViewTitleBarInternal;
    }
}
```


### interface ICoreApplicationViewTitleBarInternal

> [!IMPORTANT]
> Classic COM Interface

```MIDL
[exclusiveto(Windows.ApplicationModel.Core.CoreApplicationViewTitleBar)]
[uuid(A3AA412F-D204-4295-B7C9-42792A159251)] //10240~10583
[uuid(72558910-08E1-49C4-90BD-D2C149D1C169)] //14393~17134
[uuid(6E470D39-E79F-453C-92EF-6310EDEFD440)] //17763+
[version(NTDDI_WIN10)]
interface ICoreApplicationViewTitleBarInternal : IInspectable
{
    HRESULT OnVisibilityChanged([in] int unknown);
    HRESULT OnLayoutMetricsChanged([in] long double unknown1, [in] long double unknown2, [in] long double unknown3);
    HRESULT SetInputSinkWindow([in] HWND unknown);
    HRESULT SetTitleBarVisual([in] IUnknown* unknown);
    HRESULT HasTitleBarVisual([out] BOOL* unknown);
    [version(NTDDI_WIN10_RS1)] HRESULT NotifyPersistedValues(int unknown);
    [version(NTDDI_WIN10_RS5), propget] HRESULT DesiredTitlebarOverlayState([out, retval] DesiredTitlebarOverlayState* value);
    [version(NTDDI_WIN10_RS5), propput] HRESULT DesiredTitlebarOverlayState([in] DesiredTitlebarOverlayState value);
}
```


#### enum DesiredTitlebarOverlayState

```MIDL
[version(NTDDI_WIN10_RS5)]
typedef enum
{
    DTOS_Default = 0,
    DTOS_Visible = 1,
} DesiredTitlebarOverlayState;
```
