# Core Dispatcher

## runtimeclass Windows.UI.Core.CoreDispatcher

> [!NOTE]
> - Library: Windows.UI.dll
> - Implementation:
>     1. Windows::UI::Core::CDispatcher
>     2. Windows::UI::Core::CCoreDispatcherStatic
> - Template: Microsoft::WRL::RuntimeClass
> - Base:
>     1. member: IUnknown, IInspectable, IWeakReferenceSource, IAgileObject, IMarshal
>     2. static(WIN10_TH1+): IUnknown, IInspectable, IActivationFactory, IAgileObject

```C#
namespace Windows.UI.Core
{
    [version(NTDDI_WIN8)]
    [static(Windows.UI.Core.IInternalCoreDispatcherStatic, NTDDI_WIN10)]
    runtimeclass CoreDispatcher
    {
        [default] interface Windows.UI.Core.ICoreDispatcher;
        [version(NTDDI_WINBLUE)] interface Windows.UI.Core.ICoreDispatcherWithTaskPriority;
        [version(NTDDI_WIN10)] interface Windows.UI.Core.ICoreDispatcher2;
        interface Windows.UI.Core.ICoreAcceleratorKeys;
        interface IMessageDispatcher;
        interface IPrivateDispatcher;
        [version(NTDDI_WINBLUE)] interface IInternalDispatcher;
        [version(NTDDI_WIN10_RS3)] interface Windows.UI.Core.IInternalDispatcher2;
    }
}
```


### interface IPrivateDispatcher

> [!TIP]
> - `hasAccelerator`(`HasAcceleratorCallback`) in the function of implementation is the `bool` type, not `BOOLEAN`
> - `SetTextInputProducerExists` will assign `fExists` to `this->_fQuirkAllowNestedProcessEvents` (`bool` type)

```C#
[version(NTDDI_WIN8)]
[uuid("EF9CC6E1-96C2-4027-9120-78444953BF6F")]
interface IPrivateDispatcher : IUnknown
{
    HRESULT RegisterAcceleratorCallback([in] IAcceleratorCallback* pAccelerator);
    HRESULT UnregisterAcceleratorCallback([in] IAcceleratorCallback* pAccelerator);
    [version(NTDDI_WIN10_RS1)] HRESULT HasAcceleratorCallback([out] BOOLEAN* hasAccelerator);
    [version(NTDDI_WIN10_19H1)] HRESULT SetTextInputProducerExists([in] BOOLEAN fExists);
}
```


#### interface IAcceleratorCallback

> [!TIP]
> - Defined in Windows.UI.dll without implementation
> - `UINT8*` may be `BOOLEAN*`
> - Parameters' attributes(`[in]`, `[out]` or `[optional]`) is unknown

```C#
[version(NTDDI_WIN8)]
[uuid("8F95583E-818F-4C3B-B03D-2E6C70265F34")]
interface IAcceleratorCallback : IUnknown
{
    HRESULT PreTranslateAccelerator(MSG* pMsg, UINT8*);
    HRESULT PostTranslateAccelerator(MSG* pMsg, UINT8*);
}
```


### interface IInternalDispatcher

> [!TIP]
> - `hEventWait`(`WaitAndProcessMessages`) may be the `HANDLE` type
> - If `hEventWait` is nullptr, the `bRunAlwaysOnce`(`WaitAndProcessMessagesInternal`) will be true

```C#
[version(NTDDI_WINBLUE)]
[uuid("34FFF979-BD36-4BB1-82D2-785A605B81FB")]
[local]
interface IInternalDispatcher : IUnknown
{
    HRESULT WaitAndProcessMessages([in, optional] void* hEventWait);
    HRESULT TerminateProcessEvents();
}
```


### interface Windows.UI.Core.IInternalDispatcher2

```C#
namespace Windows.UI.Core
{
    [version(NTDDI_WIN10_RS3)]
    [uuid("C560466F-67D6-4B40-A1F3-15675E6984EC")]
    [exclusiveto(Windows.UI.Core.CoreDispatcher)]
    interface IInternalDispatcher2 : IInspectable
    {
        Windows.System.DispatcherQueue DispatcherQueue{ get; };
    }
}
```


### interface Windows.UI.Core.IInternalCoreDispatcherStatic

```C#
namespace Windows.UI.Core
{
    [version(NTDDI_WIN10)]
    [uuid("4B4D0861-D718-4F7C-BEC7-735C065F7C73")]
    [exclusiveto(Windows.UI.Core.CoreDispatcher)]
    interface IInternalCoreDispatcherStatic : IInspectable
    {
        Windows.UI.Core.CoreDispatcher GetForCurrentThread();
        [version(NTDDI_WIN10_RS1)] Windows.UI.Core.CoreDispatcher GetOrCreateForCurrentThread();
    }
}
```
