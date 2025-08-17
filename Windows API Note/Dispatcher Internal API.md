# Core Dispatcher Internal API

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


# Dispatcher Queue Internal API

> [!IMPORTANT]
> DispatcherQueue was implemented in Windows 10 Redstone 2 and has been documented since Redstone 3.

## runtimeclass Windows.System.DispatcherQueue

> [!NOTE]
> - Library: CoreMessaging.dll
> - Implementation:
>     1. Windows::System::DispatcherQueue
>     2. Windows::System::DispatcherQueueStatic
> - Template:
>     1. member: Microsoft::WRL::RuntimeClass
>     2. static: Microsoft::WRL::ActivationFactory
> - Base:
>     1. member: IUnknown, IInspectable, IWeakReferenceSource, IAgileObject, IMarshal
>     2. static: IUnknown, IInspectable, IActivationFactory, IAgileObject

> [!TIP]
> [`DispatcherQueue`](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueue) has been defined in Windows.Foundation.UniversalApiContract.winmd since Windows 10 Redstone 3.

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2)]
    [marshaling_behavior(agile), threading(both)]
    [static(Windows.System.IDispatcherQueueStatic, NTDDI_WIN10_RS2)]
    runtimeclass DispatcherQueue
    {
        [default] interface Windows.System.IDispatcherQueue;
        [version(NTDDI_WIN10_19H1)] interface Windows.System.IDispatcherQueue2;
    }
}
```

> [!CAUTION]
> **API Break:** The ordinal of functions has been changed many times.

- Windows 10 Redstone 2

```
LIBRARY CoreMessaging.dll
EXPORTS
	CreateDedicatedDispatcherQueue			@16
	CreateDispatcherQueueForCurrentThread	@17
```

- Windows 10 Redstone 3

```
LIBRARY CoreMessaging.dll
EXPORTS
	CreateDispatcherQueueForCurrentThread	@18
```

- Windows 10 Redstone 4 +

```
LIBRARY CoreMessaging.dll
EXPORTS
	CreateDispatcherQueueForCurrentThread	@19
	GetDispatcherQueueForCurrentThread		@23
```


### function CreateDedicatedDispatcherQueue

> [!CAUTION]
> **API Break:** `CreateDedicatedDispatcherQueue` has been replaced by [`CreateDispatcherQueueController`](https://learn.microsoft.com/windows/win32/api/dispatcherqueue/nf-dispatcherqueue-createdispatcherqueuecontroller) since Windows 10 Redstone 3.

> [!TIP]
> *No API Break:* [`DISPATCHERQUEUE_THREAD_APARTMENTTYPE`](https://learn.microsoft.com/windows/win32/api/dispatcherqueue/ne-dispatcherqueue-dispatcherqueue_thread_apartmenttype) is defined in <um/DispatcherQueue.h>.

```C
EXTERN_C HRESULT WINAPI CreateDedicatedDispatcherQueue(_In_ DispatcherQueueParams*, _In_ DISPATCHERQUEUE_THREAD_APARTMENTTYPE, _Deref_out_ Windows::System::IDispatcherQueue**);
```


#### struct DispatcherQueueParams

> [!CAUTION]
> **API Break:** `DispatcherQueueParams` has been removed since Windows 10 Redstone 3.

```C
struct DispatcherQueueParams; // unknown definition
```


### function CreateDispatcherQueueForCurrentThread

> [!TIP]
> `PDISPATCHERQUEUE` is defined in <um/DispatcherQueue.h>.

```C
EXTERN_C HRESULT WINAPI CreateDispatcherQueueForCurrentThread(_Deref_out_ PDISPATCHERQUEUE*);
```


### function GetDispatcherQueueForCurrentThread

```C
EXTERN_C HRESULT WINAPI GetDispatcherQueueForCurrentThread(_Deref_out_ PDISPATCHERQUEUE*);
```


### interface Windows.System.IDispatcherQueueStatic

> [!CAUTION]
> **API Break:**
> 1. The IID of this interface has been changed since Windows 10 Redstone 3.
> 2. The DISPID of functions has been changed since Windows 10 Redstone 3.
> 3. `TryGetForCurrentThread` has been renamed to [`GetForCurrentThread`](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueue.getforcurrentthread) since Windows 10 Redstone 3.

> [!TIP]
> `IDispatcherQueueStatic` has been defined in Windows.Foundation.UniversalApiContract.winmd since Windows 10 Redstone 3.

- Windows 10 Redstone 2

```C#
namespace Windows.System
{
    [uuid("B9E03CF6-3583-4A19-87FB-61AB98E9FEE8"), version(NTDDI_WIN10_RS2)]
    [exclusiveto(Windows.System.DispatcherQueue)]
    interface IDispatcherQueueStatic : IInspectable
    {
        [deprecated("", remove, NTDDI_WIN10_RS3)] Windows.Foundation.IAsyncOperation<Windows.System.DispatcherQueue> CreateDedicatedQueueAsync(Windows.System.IDispatcherQueueOptions options);
        Windows.System.DispatcherQueue TryGetForCurrentThread();
    }
}
```


### interface Windows.System.IDispatcherQueue

> [!CAUTION]
> **API Break:** `RunAsync` has been replaced by [`TryEnqueue`](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueue.tryenqueue) since Windows 10 Redstone 3.

> [!TIP]
> `IDispatcherQueue` has been defined in Windows.Foundation.UniversalApiContract.winmd since Windows 10 Redstone 3.

- Windows 10 Redstone 2

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2)]
    [uuid("603E88E4-A338-4FFE-A457-A5CFB9CEB899")]
    [exclusiveto(Windows.System.DispatcherQueue)]
    interface IDispatcherQueue : IInspectable
    {
        Windows.System.DispatcherQueueTimer CreateTimer();
        [deprecated("", remove, NTDDI_WIN10_RS3)] [overload("RunAsync")] Windows.Foundation.IAsyncAction RunAsync(Windows.System.DispatcherQueueHandler callback);
        [deprecated("", remove, NTDDI_WIN10_RS3)] [overload("RunAsync")] Windows.Foundation.IAsyncAction RunWithPriorityAsync(Windows.System.DispatcherQueueHandler callback, Windows.System.DispatcherQueuePriority priority);
        [deprecated("", remove, NTDDI_WIN10_RS3)] [overload("RunAsync")] Windows.Foundation.IAsyncAction RunTaskAsync(Windows.System.DispatcherQueueAsyncHandler callback);
        [deprecated("", remove, NTDDI_WIN10_RS3)] [overload("RunAsync")] Windows.Foundation.IAsyncAction RunTaskWithPriorityAsync(Windows.System.DispatcherQueueAsyncHandler callback, Windows.System.DispatcherQueuePriority priority);
        [deprecated("", remove, NTDDI_WIN10_RS3)] void StopProcessEvents();
    }
}
```


#### delegate Windows.System.DispatcherQueueHandler

> [!TIP]
> [`DispatcherQueueHandler`](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueuehandler) exists in the leatest Windows.

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2)]
    [uuid("")] // unknown GUID in RS2
    delegate void DispatcherQueueHandler();
}
```


#### delegate Windows.System.DispatcherQueueAsyncHandler

> [!CAUTION]
> **API Break:** `DispatcherQueueAsyncHandler` has been removed since Windows 10 Redstone 3.

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2), deprecated("", remove, NTDDI_WIN10_RS3)]
    [uuid("")] // unknown GUID
    delegate Windows.Foundation.IAsyncAction DispatcherQueueAsyncHandler();
}
```


#### enum Windows.System.DispatcherQueuePriority

> [!CAUTION]
> **API Break:** [`DispatcherQueuePriority`](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueuehandler) has been changed since Windows 10 Redstone 3.

> [!TIP]
> `DispatcherQueuePriority` has been defined in Windows.Foundation.UniversalApiContract.winmd since Windows 10 Redstone 3.

- Windows 10 Redstone 2

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2)]
    enum DispatcherQueuePriority
    {
        [deprecated("", remove, NTDDI_WIN10_RS3)] None = 0,
        [deprecated("", remove, NTDDI_WIN10_RS3)] Low = 1,
        [deprecated("", remove, NTDDI_WIN10_RS3)] Normal = 2,
        [deprecated("", remove, NTDDI_WIN10_RS3)] High = 3
    };
}
```


## runtimeclass DispatcherQueueOptions

> [!NOTE]
> - Library: CoreMessaging.dll
> - Implementation: Windows::System::DispatcherQueueOptions
> - Template: Microsoft::WRL::RuntimeClass
> - Base: IUnknown IInspectable IWeakReferenceSource IAgileObject IMarshal

> [!CAUTION]
> **API Break:**
> 1. `DispatcherQueueOptions` in Windows 10 Redstone 2 has been renamed to [`DispatcherQueueController`](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueuecontroller) since Windows 10 Redstone 3.
> 2. [`DispatcherQueueOptions`](https://learn.microsoft.com/windows/win32/api/dispatcherqueue/ns-dispatcherqueue-dispatcherqueueoptions) in Windows 10 Redstone 3 is an other API.

> [!TIP]
> `DispatcherQueueController` has been defined in Windows.Foundation.UniversalApiContract.winmd since Windows 10 Redstone 3.

- Windows10 Redstone 2

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2), deprecated("", remove, NTDDI_WIN10_RS3)]
    runtimeclass DispatcherQueueOptions
    {
        [default] interface Windows.System.IDispatcherQueueOptions;
    }
}
```

- Windows 10 Redstone 3

```
LIBRARY CoreMessaging.dll
EXPORTS
	CreateDispatcherQueueController	@17
```

- Windows 10 Redstone 4 +

```
LIBRARY CoreMessaging.dll
EXPORTS
	CreateDispatcherQueueController	@18
```


### interface Windows.System.IDispatcherQueueOptions

> [!CAUTION]
> **API Break:** `IDispatcherQueueOptions` has been renamed to `IDispatcherQueueController` since Windows 10 Redstone 3.

> [!TIP]
> `IDispatcherQueueController` has been defined in Windows.Foundation.UniversalApiContract.winmd since Windows 10 Redstone 3.

- Windows 10 Redstone 2

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2)]
    [uuid("22F34E66-50DB-4E36-A98D-61C01B384D20")]
    [exclusiveto(Windows.System.DispatcherQueueOptions)]
    interface IDispatcherQueueOptions : IInspectable
    {
        [deprecated("", remove, NTDDI_WIN10_RS3)] event Windows.Foundation.TypedEventHandler<Windows.System.DispatcherQueueOptions, IInspectable> Completed;
        [deprecated("", remove, NTDDI_WIN10_RS3)] event Windows.Foundation.TypedEventHandler<Windows.System.DispatcherQueueOptions, Windows.System.DispatcherQueueInitializedEventArgs> Initialized;
    }
}
```


#### runtimeclass Windows.System.DispatcherQueueInitializedEventArgs

> [!NOTE]
> - Library: CoreMessaging.dll
> - Implementation: Windows::System::DispatcherQueueInitializedEventArgs
> - Template: Microsoft::WRL::RuntimeClass
> - Base: IUnknown IInspectable IWeakReferenceSource IAgileObject IMarshal

> [!CAUTION]
> **API Break:** `DispatcherQueueInitializedEventArgs` has been removed since Windows 10 Redstone 3.

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2), deprecated("", remove, NTDDI_WIN10_RS3)]
    runtimeclass DispatcherQueueInitializedEventArgs
    {
        [default] interface Windows.System.IDispatcherQueueInitializedEventArgs;
    }
}
```


##### interface Windows.System.IDispatcherQueueInitializedEventArgs

> [!CAUTION]
> **API Break:** `IDispatcherQueueInitializedEventArgs` has been removed since Windows 10 Redstone 3.

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2), deprecated("", remove, NTDDI_WIN10_RS3)]
    [uuid("67CC0CDA-8FC3-46CC-9730-8FE0B356044C")]
    [exclusiveto(Windows.System.DispatcherQueueInitializedEventArgs)]
    interface IDispatcherQueueInitializedEventArgs : IInspectable
    {
        Windows.System.DispatcherQueue DispatcherQueue{ get; };
    }
}
```


## runtimeclass Windows.System.DispatcherQueueTimer

> [!NOTE]
> - Library: CoreMessaging.dll
> - Implementation: Windows::System::DispatcherQueueTimer
> - Template: Microsoft::WRL::RuntimeClass
> - Base: IUnknown IInspectable IWeakReferenceSource IAgileObject IMarshal

> [!TIP]
> *No API Break*: [`DispatcherQueueTimer`](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueuetimer) has been defined in Windows.Foundation.UniversalApiContract.winmd since Windows 10 Redstone 3.

- Windows 10 Redstone 2

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2)]
    [marshaling_behavior(agile)]
    runtimeclass DispatcherQueueTimer
    {
        [default] interface Windows.System.IDispatcherQueueTimer;
    }
}
```


### interface Windows.System.IDispatcherQueueTimer

> [!CAUTION]
> **API Break:** Since Windows 10 Redstone 3, the DISPID of functions(`Tick`, `Start`, `Stop`) has been changed and you can find the definition in Windows.Foundation.UniversalApiContract.winmd.

> [!TIP]
> *No API Break*: `IsEnabled` has been renamed to `IsRunning`[](https://learn.microsoft.com/uwp/api/windows.system.dispatcherqueuetimer.isrunning) since Windows 10 Redstone 3.

- Windows 10 Redstone 2

```C#
namespace Windows.System
{
    [version(NTDDI_WIN10_RS2)]
    [uuid("5FEABB1D-A31C-4727-B1AC-37454649D56A")]
    [exclusiveto(Windows.System.DispatcherQueueTimer)]
    interface IDispatcherQueueTimer : IInspectable
    {
        Windows.Foundation.TimeSpan Interval{ get; set; };
        Boolean IsEnabled{ get; };
        Boolean IsRepeating{ get; set; };
        event Windows.Foundation.TypedEventHandler<Windows.System.DispatcherQueueTimer, IInspectable> Tick;
        void Start();
        void Stop();
    }
}
```
