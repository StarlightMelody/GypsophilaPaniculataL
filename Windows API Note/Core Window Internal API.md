# Core Window Internal API

## runtimeclass Windows.UI.Core.CoreWindow

### interface IPrivateCoreWindow

> [!CAUTION]
> **API Break:**
> 1. The IID has been changed. If you want use this interface, please use correct `uuid`, according to `version` attribute.
> 2. The DISPID of functions has been changed. If you want use this interface in older Windows, please delete redundant declarations, according to `version` attribute.
> 3. Some functions have been removed. If you want use this interface in newer Windows, please delete redundant declarations, according to `deprecated` attribute.

```C#
[uuid("1927A176-0C11-43FE-BB80-3189B19F7819"), version(NTDDI_WIN8)]
[uuid("2127BEE7-8704-4FC6-8878-61C7334682D3"), version(NTDDI_WINBLUE)]
[uuid("CD98A184-5273-44AC-BF52-D62342A94BD5"), version(NTDDI_WIN10)]
interface IPrivateCoreWindow : IUnknown
{
    [propget] HRESULT MayDuplicate([out, retval] BOOLEAN* value);
    HRESULT NotifyOnFirstActivation([in] HWND hwndSink);
    [propget] HRESULT MainWindow([out, retval] BOOLEAN* value);
    [propput] HRESULT MainWindow([in] BOOLEAN value);
    [version(NTDDI_WIN10_RS4)] [propget] HRESULT IsUWP([out, retval] BOOLEAN* value);
    [propput] HRESULT VisibilityDelay([in] DWORD value);
    [version(NTDDI_WINBLUE)] HRESULT OnPreSuspending();
    [version(NTDDI_WINBLUE)] HRESULT OnPostResuming();
    [version(NTDDI_WIN10), deprecated("", remove, NTDDI_WIN10_RS2)] HRESULT SetTextInputDelegationPID([in] DWORD uiPID, [in] DWORD uiDelegatePID);
}
```


### interface Windows.UI.Core.IInternalCoreWindow

> [!CAUTION]
> **API Break:**
> 1. The IID has been changed. If you want use this interface, please use correct `uuid`, according to `version` attribute.
> 2. The DISPID of functions has been changed. If you want use this interface in older Windows, please delete redundant declarations, according to `version` attribute.

```C#
namespace Windows.UI.Core
{
    [uuid("2CB080DE-2CB4-4DA7-AD5F-1068803CE391"), version(NTDDI_WIN8)]
    [uuid("2B97A9ED-C11E-47F6-9F84-2EA2E63E9822"), version(NTDDI_WINBLUE)]
    [uuid("42A17E3D-7171-439A-B1FA-A31B7B957489"), version(NTDDI_WIN10)]
    interface IInternalCoreWindow : IInspectable
    {
        Windows.Devices.Input.MouseDevice MouseDevice{ get; };
        Windows.UI.ViewManagement.ApplicationViewState ApplicationViewState{ get; };
        [version(NTDDI_WINBLUE)] Windows.UI.ViewManagement.ApplicationViewOrientation ApplicationViewOrientation{ get; };
        [version(NTDDI_WINBLUE)] UInt32/*ADJACENT_DISPLAY_EDGES*/ AdjacentDisplayEdges{ get; };
        [version(NTDDI_WINBLUE)] Boolean IsOnLockScreen{ get; };
        Windows.UI.Input.PointerVisualizationSettings PointerVisualizationSettings{ get; };
        Windows.UI.Core.CoreWindowResizeManager CoreWindowResizeManager{ get; };
        [version(NTDDI_WINBLUE)] Boolean IsScreenCaptureEnabled{ get; set; };
        [version(NTDDI_WIN10)] Windows.Phone.UI.Core.FULL_SCREEN_TYPE SuppressSystemOverlays{ get; set; };
        void OnMouseDeviceListenerChange();
        event Windows.UI.Core.IThemeChangedEventHandler ThemeChanged;
        event Windows.UI.Core.ContextMenuRequestedEventHandler ContextMenuRequested;
        event Windows.UI.Core.IDisplayChangedEventHandler DisplayChanged;
        [version(NTDDI_WINBLUE)] event Windows.UI.Core.IConsolidatedEventHandler Consolidated;
    }
}
```


## runtimeclass Windows.UI.Core.CoreWindowResizeManager

> [!NOTE]
> - Implementation:
>     1. Windows::UI::Core::CCoreWindowResizeManager $\leftarrow$ Microsoft::WRL::RuntimeClass
>     2. Windows::UI::Core::CCoreWindowResizeManagerStatics $\leftarrow$ Microsoft::WRL::AgileActivationFactory
> - Base :
>     1. interface: IUnknown, IInspectable, IWeakReferenceSource
>     2. static: IUnknown, IInspectable, IActivationFactory
> - Library: Windows.UI.dll

```C#
[marshaling_behavior(agile)]
[static(Windows.UI.Core.ICoreWindowResizeManagerStatics, NTDDI_WIN8)]
[version(NTDDI_WIN8)]
runtimeclass CoreWindowResizeManager
{
    [default] interface Windows.UI.Core.ICoreWindowResizeManager;
    [version(NTDDI_WINBLUE)] interface Windows.UI.Core.ICoreWindowResizeManagerLayoutCapability;
    [version(NTDDI_WIN10_RS2)] interface IPrivateCoreWindowFrameworkSynchronizedResize;
}
```


### interface IPrivateCoreWindowFrameworkSynchronizedResize

```C#
[local]
[uuid("D1498437-3BAC-4BE5-96CB-F6AD1FA6C4F4")]
[version(NTDDI_WIN10_RS2)]
interface IPrivateCoreWindowFrameworkSynchronizedResize : IUnknown
{
    [propput] HRESULT SynchronizedResize([in]BOOLEAN value);
    [propget] HRESULT SynchronizedResize([out, retval] BOOLEAN* value);
    HRESULT GetResizeDCompSynchronizationObject([out] HANDLE* phDCompSyncObject);
}
```
