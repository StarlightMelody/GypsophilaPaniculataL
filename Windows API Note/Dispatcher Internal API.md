# WinRT Dispatcher Internal API

## runtimeclass Windows.UI.Core.CoreDispatcher
- Implementation: Windows::UI::Core::CDispatcher & Windows::UI::Core::CCoreDispatcherStatic
- Library: Windows.UI.dll
```MIDL
namespace Windows.UI.Core
{
    [static(IUnknown, NTDDI_WIN10)]
    [static(IInspectable, NTDDI_WIN10)]
    [static(IActivationFactory, NTDDI_WIN10)]
    [static(Windows.UI.Core.IInternalCoreDispatcherStatic, NTDDI_WIN10)]
    [static(IAgileObject, NTDDI_WIN10)]
    [version(NTDDI_WIN8)]
    runtimeclass CoreDispatcher
    {
        interface IUnknown;
        interface IInspectable;
        [default] interface Windows.UI.Core.ICoreDispatcher;
        interface IWeakReferenceSource;
        [version(NTDDI_WINBLUE)] interface Windows.UI.Core.ICoreDispatcherWithTaskPriority;
        [version(NTDDI_WIN10)] interface Windows.UI.Core.ICoreDispatcher2;
        interface Windows.UI.Core.ICoreAcceleratorKeys;
        interface IMessageDispatcher;
        interface IPrivateDispatcher;
        [version(NTDDI_WINBLUE)] interface IInternalDispatcher;
        [version(NTDDI_WIN10_RS3)] interface Windows.UI.Core.IInternalDispatcher2;
        interface IAgileObject;
        interface IMarshal;
    }
}
```

### interface IPrivateDispatcher
- hasAccelerator(HasAcceleratorCallback) in the function of implementation is the bool type, not BOOLEAN(unsigned int8)
- SetTextInputProducerExists will assign fExists to this->_fQuirkAllowNestedProcessEvents (bool type)
```MIDL
[uuid(EF9CC6E1-96C2-4027-9120-78444953BF6F)]
[version(NTDDI_WIN8)]
interface IPrivateDispatcher : IUnknown
{
    HRESULT RegisterAcceleratorCallback([in] IAcceleratorCallback* pAccelerator);
    HRESULT UnregisterAcceleratorCallback([in] IAcceleratorCallback* pAccelerator);
    [version(NTDDI_WIN10_RS1)] HRESULT HasAcceleratorCallback([out] BOOLEAN* hasAccelerator);
    [version(NTDDI_WIN10_19H1)] HRESULT SetTextInputProducerExists([in] BOOLEAN fExists);
}
```

#### interface IAcceleratorCallback
- Defined in Windows.UI.dll without implementation
- UINT8* may be BOOLEAN*
- Parameters' attributes([in], [out] or [optional]) is unknown
```MIDL
[uuid(8F95583E-818F-4C3B-B03D-2E6C70265F34)]
[version(NTDDI_WIN8)]
interface IAcceleratorCallback : IUnknown
{
    HRESULT PreTranslateAccelerator(MSG* pMsg, UINT8*);
    HRESULT PostTranslateAccelerator(MSG* pMsg, UINT8*);
}
```

### interface IInternalDispatcher
- hEventWait(WaitAndProcessMessages) may be the HANDLE type
- If hEventWait is nullptr, the bRunAlwaysOnce(WaitAndProcessMessagesInternal) will be true
```MIDL
[local]
[uuid(34FFF979-BD36-4BB1-82D2-785A605B81FB)]
[version(NTDDI_WINBLUE)]
interface IInternalDispatcher : IUnknown
{
    HRESULT WaitAndProcessMessages([in, optional] void* hEventWait);
    HRESULT TerminateProcessEvents();
}
```

### interface Windows.UI.Core.IInternalDispatcher2
```MIDL
namespace Windows.UI.Core
{
    [exclusiveto(Windows.UI.Core.CoreDispatcher)]
    [uuid(C560466F-67D6-4B40-A1F3-15675E6984EC)]
    [version(NTDDI_WIN10_RS3)]
    interface IInternalDispatcher2 : IInspectable
    {
        Windows.System.DispatcherQueue DispatcherQueue{ get; };
    }
}
```

### interface Windows.UI.Core.IInternalCoreDispatcherStatic
```MIDL
namespace Windows.UI.Core
{
    [exclusiveto(Windows.UI.Core.CoreDispatcher)]
    [uuid(4B4D0861-D718-4F7C-BEC7-735C065F7C73)]
    [version(NTDDI_WIN10)]
    interface IInternalCoreDispatcherStatic : IInspectable
    {
        Windows.UI.Core.CoreDispatcher GetForCurrentThread();
        [version(NTDDI_WIN10_RS1)] Windows.UI.Core.CoreDispatcher GetOrCreateForCurrentThread();
    }
}
```
