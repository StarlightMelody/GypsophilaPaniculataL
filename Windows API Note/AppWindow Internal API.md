# AppWindow Internal API

## runtimeclass Windows.Internal.UI.WindowManagement.HmonitorInterop

> [!NOTE]
> - Implementation: Windows::Internal::UI::WindowManagement::HmonitorInteropStatics $\leftarrow$ Microsoft::WRL::ActivationFactory
> - Base : IUnknown, IInspectable, IActivationFactory, IAgileObject, IMarshal
> - Library: WindowManagementAPI.dll

```MIDL
namespace Windows.Internal.UI.WindowManagement
{
    [static(IHmonitorInteropStatics, NTDDI_WIN10_VB)]
    [version(NTDDI_WIN10_VB)]
    runtimeclass HmonitorInterop{ }
}
```


### interface Windows.Internal.UI.WindowManagement.IHmonitorInteropStatics

```MIDL
namespace Windows.Internal.UI.WindowManagement
{
    [uuid(C3795793-0C2E-5FA2-9D7E-A71A778B0FE9)]
    [version(NTDDI_WIN10_VB)]
    interface IHmonitorInteropStatics : IInspectable
    {
        UInt64/*HMONITOR*/ GetForUIContext(Windows.UI.UIContext context);
    }
}
```
