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
