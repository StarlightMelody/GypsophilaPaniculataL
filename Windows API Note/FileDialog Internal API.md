# FileDialog Internal API

## Out-of-Proc FileDialog

### BrokerFileDialog.dll
CLSCTX_INPROC_SERVER
| CLSID                                  | Symbol                           | CoClass                                                |
| ---                                    | ---                              | ---                                                    |
| {3217B1B1-5DC3-4590-9C62-EF9E2DF1C25D} | CLSID_BrokerFileOpenDialog       | Windows.Security.Isolation.BrokerFileOpenDialog        |
| {34F40FF6-2222-4F38-8298-459707ED7A27} | CLSID_BrokerFileOpenDialogLegacy | Windows.Security.Isolation.BrokerFileOpenDialogLegacy  |
| {86FCA1b6-0A22-4652-9480-08F27C947B0F} | CLSID_BrokerFileSaveDialog       | Windows.Security.Isolation.BrokerFileSaveDialog        |
| {22CF69E9-57ED-47F8-AB4D-0418F4A2A06B} | CLSID_BrokerFileSaveDialogLegacy | Windows.Security.Isolation.BrokerFileSaveDialogLegacy  |
| {06A5E346-4DEF-5F5B-D142-24613E0E3296} | CLSID_BrokerShellObject          | Windows.Security.Isolation.BrokerShellObject           |
| {6C2241BA-47B6-50D8-53E9-A5b61090A5EE} | CLSID_BrowseForFolderCallback    | Windows.Security.Isolation.BrowseForFolderCallback     |
### FileDialogBroker.exe
CLSCTX_LOCAL_SERVER
| CLSID                                  | Symbol                           | CoClass                                                |
| ---                                    | ---                              | ---                                                    |
| {7394A3BB-E76A-4244-8534-132593937AD1} | CLSID_FileOpenDialogBroker       | Windows.Security.Isolation.FileOpenDialogBroker        |
| {52D1ACF4-CD13-4B51-ABBF-B65AF636D0E3} | CLSID_FileOpenDialogLegacyBroker | Windows.Security.Isolation.FileOpenDialogLegacyBroker  |
| {3CAE7212-964B-4379-B37C-E11999B4405C} | CLSID_FileSaveDialogBroker       | Windows.Security.Isolation.FileSaveDialogBroker        |
| {E1C134F1-B29F-48C0-905C-B637DF41384E} | CLSID_FileSaveDialogLegacyBroker | Windows.Security.Isolation.FileSaveDialogLegacyBroker  |
| {601C2B23-B244-5C3A-546A-433F5C42E928} | CLSID_ShellObjectBroker          | Windows.Security.Isolation.ShellObjectBroker           |

### Sample:
```C++
#include <ShObjIdl_core.h>
#include <winrt/base.h>
int main()
{
    winrt::init_apartment();
    winrt::com_ptr<::IFileOpenDialog> dlg{ winrt::create_instance<::IFileOpenDialog>(winrt::guid(L"{3217B1B1-5DC3-4590-9C62-EF9E2DF1C25D}"), CLSCTX_INPROC_SERVER) };
    winrt::check_hresult(dlg->Show(HWND_DESKTOP));
}
```
