# XAML Hosted Window Internal API

## runtimeclass Windows.Internal.UI.Dialogs.XamlHostedDialog

> [!CAUTION]
> **API Break:** In Build 22000 Insider Version, the declaration of this interface updated by LCU. The following declaration is suitable for Build 22000 Release Version.

> [!NOTE]
> - Implementation: winrt::Windows::Internal::UI::Dialogs::implementation::XamlHostedDialog $\leftarrow$ winrt::implements
> - Base :
>     1. interface: IUnknown, IInspectable, IWeakReferenceSource, IAgileObject, IMarshal
>     2. static: IUnknown, IInspectable, IWeakReferenceSource, IAgileObject, IMarshal, IActivationFactory
> - Library: Windows.Internal.UI.Dialogs.dll

```C#
namespace Windows.Internal.UI.Dialogs
{
    [static(Windows.Internal.UI.Dialogs.IXamlHostedDialogStatics, NTDDI_WIN10_CO)]
    [version(NTDDI_WIN10_CO)]
    runtimeclass XamlHostedDialog
    {
        [default] interface Windows.Internal.UI.Dialogs.IXamlHostedDialog;
        interface Windows.Internal.UI.Dialogs.IXamlHostedConfig;
        interface IDesktopWindowXamlSourceNative2;
        interface Windows.Internal.UI.Dialogs.IXamlHostedDialogExtendedContent;
    }
}
```


### interface Windows.Internal.UI.Dialogs.IXamlHostedDialog

> [!CAUTION]
> **API Break:**
> 1. The IID has been changed. If you want use this interface, please use correct `uuid`, according to `version` attribute.
> 2. The DISPID of functions has been changed. If you want use this interface in older Windows, please delete redundant declarations, according to `version` attribute.

```C#
namespace Windows.Internal.UI.Dialogs
{
    [uuid("AF06396A-8874-506C-B930-DF54B3CF6C27"), version(NTDDI_WIN10_CO)]
    [uuid("C910EC99-A562-55F0-916B-2C75E5CCBB48"), version(NTDDI_WIN10_NI)]
    [uuid("C6E6E4F7-CBA2-55E1-9D0E-292F0ADA8E5D"), version(NTDDI_WIN11_ZN)]
    interface IXamlHostedDialog : IInspectable
    {
        HostedDialogType DialogType{ get; };
        UInt64 XamlWindow{ get; };
        Windows.UI.Xaml.UIElement XamlContent{ get; set; };
        String Title{ get; set; };
        String ContentString{ get; set; };
        event Windows.Foundation.EventHandler<XamlHostedDialogCommandInvokedArgs> CommandInvoked;
        event Windows.Foundation.EventHandler<XamlHostedDialogCommandInvokedArgs> DesiredSizeChanged;
        UInt32 MinCommandCount{get; set;};
        UInt32 MaxCommandCount{ get; set; };
        UInt32 DefaultCommandIndex{ get; set; };
        UInt32 CancelCommandIndex{ get; set; };
        Windows.Foundation.Size Position{ get; set; };
        Windows.Foundation.Size WindowSize{ get; set; };
        void Measure(Windows.Foundation.Size value);
        void Initialize(Boolean value1, Boolean value2);
        void Shutdown();
        void Show();
        [version(NTDDI_WIN10_NI)] void Show(Boolean value);
        void Hide();
        void ShowTitle(Boolean value);
        void SetPopupCommands(Windows.Foundation.Collections.IVector<String> value);
        Boolean UseAppTheme{ get; set; };
        [version(NTDDI_WIN10_NI)] Boolean UseXamlShadows{ get; set; };
        [version(NTDDI_WIN10_NI)] Boolean AllowTextWrapping{ get; set; };
        [version(NTDDI_WIN10_NI)] Boolean HasFocus{ get; };
        [version(NTDDI_WIN10_NI)] void SetFocus(Boolean value);
        [version(NTDDI_WIN10_NI)] Boolean DisableButtonInteraction{ get; set; };
        [version(NTDDI_WIN11_ZN)] Boolean TransparentBackground{ get; set; };
        [version(NTDDI_WIN11_ZN)] event Windows.Foundation.EventHandler<XamlHostedDialogCommandInvokedArgs> FirstFrameRendered;
        [version(NTDDI_WIN11_ZN)] Boolean UsePadding{ get; set; };
    }
}
```


#### enum Windows.Internal.UI.Dialogs.HostedDialogType

```C#
namespace Windows.Internal.UI.Dialogs
{
    [flags]
    [version(NTDDI_WIN10_CO)]
    enum HostedDialogType
    {
        HostedDialog = 0,
        HostedMessageDialog = 1,
        [version(NTDDI_WIN11_ZN)] Flyout = 2
    };
}
```


#### runtimeclass Windows.Internal.UI.Dialogs.XamlHostedDialogCommandInvokedArgs

```C#
namespace Windows.Internal.UI.Dialogs
{
    [version(NTDDI_WIN10_CO)]
    runtimeclass XamlHostedDialogCommandInvokedArgs
    {
        [default] interface IXamlHostedDialogCommandInvokedArgs;
    }
}
```


##### interface Windows.Internal.UI.Dialogs.IXamlHostedDialogCommandInvokedArgs

> [!CAUTION]
> **API Break:** The IID has been changed. If you want use this interface, please use correct `uuid`, according to `version` attribute.

```C#
namespace Windows.Internal.UI.Dialogs
{
    [exclusiveto(Windows.Internal.UI.Dialogs.XamlHostedDialogCommandInvokedArgs)]
    [uuid("A8914AB1-A808-56DB-A0FD-1F147C041ADD"), version(NTDDI_WIN10_CO)]
    [uuid("0E7FB54E-0909-57FD-9ABE-579B9ECF1023"), version(NTDDI_WIN10_NI)]
    interface IXamlHostedDialogCommandInvokedArgs : IInspectable
    {
        UInt32 CommandIndex{ get; };
        [version(NTDDI_WIN10_NI)] Boolean WasHyperlinkInvoked{ get; };
    }
}
```


### interface Windows.Internal.UI.Dialogs.IXamlHostedDialogStatics

> [!CAUTION]
> **API Break:** The IID has been changed. If you want use this interface, please use correct `uuid`, according to `version` attribute.

```C#
namespace Windows.Internal.UI.Dialogs
{
    [uuid("2AE8CB57-6A0A-50FE-B988-90929FEF9DE1"), version(NTDDI_WIN10_CO)]
    [uuid("BA7592B6-7402-54A4-9ED0-99F9E0680872"), version(NTDDI_WIN11_ZN)]
    interface IXamlHostedDialogStatics : IInspectable
    {
        Windows.Internal.UI.Dialogs.XamlHostedDialog CreateHostedDialog(UInt64 hWnd);
        Windows.Internal.UI.Dialogs.XamlHostedDialog CreateHostedMessageDialog(UInt64 hWnd);
        Windows.Internal.UI.Dialogs.XamlHostedDialog CreateHostedMessageDialogWithExtendedContent(UInt64 hWnd);
        [version(NTDDI_WIN11_ZN)] Windows.Internal.UI.Dialogs.XamlHostedDialog CreateFlyout(UInt64 hWnd);
    }
}
```


### interface Windows.Internal.UI.Dialogs.IXamlHostedConfig

```C#
namespace Windows.Internal.UI.Dialogs
{
    [uuid("9702085D-3F86-5D06-B287-A1DDDADAD9DA")]
    [version(NTDDI_WIN10_CO)]
    interface IXamlHostedConfig : IInspectable
    {
        void AddMetadataProvider(IInspectable value);
        void AddPriFileReference(String value);
    }
}
```


### interface Windows.Internal.UI.Dialogs.IXamlHostedDialogExtendedContent

> [!CAUTION]
> **API Break:** The IID has been changed. If you want use this interface, please use correct `uuid`, according to `version` attribute.

```C#
namespace Windows.Internal.UI.Dialogs
{
    [uuid("B08F06ED-8E38-59A2-B9AD-D9A7DF321635"), version(NTDDI_WIN10_CO)]
    [uuid("84759A40-F886-5D22-92D0-B120F8367AFE"), version(NTDDI_WIN10_NI)]
    interface IXamlHostedDialogExtendedContent : IInspectable
    {
        String ContentStringPrimary{ get; set; };
        String ContentStringSecondary{ get; set; };
        String Glyph{ get; set; };
        String GlyphFont{ get; set; };
        [version(NTDDI_WIN10_NI)] Windows.UI.Xaml.UIElement InnerXamlContent{ get; set; };
        [version(NTDDI_WIN10_NI)] String Hyperlink{ get; set; };
    }
}
```
