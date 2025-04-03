# WinRT XAML Presenter

## runtimeclass Windows.UI.Xaml.Hosting.XamlPresenter
- Implementation:
    - DirectUI::XamlPresenter
    - DirectUI::XamlPresenterGenerated
    - DirectUI::XamlPresenterFactory
- Library: Windows.UI.Xaml.dll
- Unknown interface name:
    - IID_A205D5C9-7BFF-4B14-B138-E415D49E1095 is a GUID from DirectUI::XamlPresenterGenerated, this interface doesn't export new member functions
    - IID_3F184A52-B00F-4541-8B25-489E9FE1543D is a GUID from ctl::WeakReferenceSource
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [static(Windows.UI.Xaml.Hosting.IXamlPresenterStatics, NTDDI_WINBLUE)]
    [static(Windows.UI.Xaml.Hosting.IXamlPresenterStatics2, NTDDI_WIN10)]
    [static(Windows.UI.Xaml.Hosting.IXamlPresenterStatics3, NTDDI_WIN10_RS4)]
    [static(IActivationFactory, NTDDI_WINBLUE)]
    [static(IAgileObject, NTDDI_WIN10_RS4)]
    [static(ISupportErrorInfo, NTDDI_WINBLUE)]
    [static(IUnknown, NTDDI_WINBLUE)]
    [static(IInspectable, NTDDI_WINBLUE)]
    [static(IMarshal, NTDDI_WINBLUE)]
    [version(NTDDI_WINBLUE)]
    runtimeclass XamlPresenter
    {
        interface IXamlPresenterResources;
        [version(NTDDI_WIN10)] interface IID_A205D5C9-7BFF-4B14-B138-E415D49E1095;
        [default] interface Windows.UI.Xaml.Hosting.IXamlPresenter;
        [version(NTDDI_WIN10)] interface Windows.UI.Xaml.Hosting.IXamlPresenterPrivate;
        [version(NTDDI_WIN10)] interface Windows.UI.Xaml.Hosting.IXamlPresenter2;
        [version(NTDDI_WIN10_19H1)] interface Windows.UI.Xaml.Hosting.IXamlPresenter4;
        [version(NTDDI_WIN10_RS4)] interface IID_3F184A52-B00F-4541-8B25-489E9FE1543D；
        interface IWeakReferenceSource;
        interface IReferenceTracker;
        [version(NTDDI_WIN10)] interface Windows.UI.Xaml.Hosting.IReferenceTrackerInternal;
        interface ISupportErrorInfo;
        interface IUnknown;
        interface IInspectable;
        interface IMarshal;
    }
}
```

### interface IXamlPresenterResources
```MIDL
[uuid(04D09167-1945-43AC-A0A9-B1AED01BE2D8)]
[version(NTDDI_WINBLUE)]
interface IXamlPresenterResources : IUnknown
{
    HRESULT SetResourceManager([in] IMrtResourceManager* pResourceManager);
}
```

### interface Windows.UI.Xaml.Hosting.IXamlPresenter
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlPresenter)]
    [uuid(8438B07A-9CE8-4E22-AB5D-811D84699566)]
    [version(NTDDI_WINBLUE)]
    interface IXamlPresenter : IInspectable
    {
        Windows.UI.Xaml.UIElement Content{ get; set; };
        void SetAtlasSizeHint(UInt32 width, UInt32 height);
        void InitializePresenter();
    }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlPresenterPrivate
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlPresenter)]
    [uuid(62D7B5F2-2EAF-4CCD-BB91-87AD6E01C92D)]
    [version(NTDDI_WIN10)]
    interface IXamlPresenterPrivate : IInspectable
    {
        void SetViewActivityState(Boolean active , Boolean allowDWMSnapshot);
    }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlPresenter2
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlPresenter)]
    [uuid(1114F710-6D30-4572-B24E-C81CF25F0FA5)]
    [version(NTDDI_WIN10)]
    interface IXamlPresenter2 : IInspectable
    {
        Windows.UI.Xaml.ResourceDictionary Resources{ get; set; };
        Windows.Foundation.Rect Bounds{ get; };
        Windows.UI.Xaml.ApplicationTheme RequestedTheme{ get; set; };
        Boolean TransparentBackground{ get; set; };
        void InitializePresenterWithTheme(Windows.UI.Xaml.ApplicationTheme requestedTheme);
        void SetCaretWidth(Int32 width);
    }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlPresenter4
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlPresenter)]
    [uuid(59BFB2B6-68A6-515F-9AE8-3BF645F123E7)]
    [version(NTDDI_WIN10_19H1)]
    interface IXamlPresenter4 : IInspectable
    {
        void SetFontScale(Single fontScale);
    }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlPresenterStatics
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlPresenter)]
    [uuid(5C6EF05E-F60D-4433-8BC6-40586456AFEB)]
    [version(NTDDI_WINBLUE)]
    interface IXamlPresenterStatics : IInspectable
    {
        XamlPresenter CreateFromHwnd(Int32 hwnd);
    }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlPresenterStatics2
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlPresenter)]
    [uuid(D0C1E6C3-1D35-4770-9C3B-E3FF2EEFCC25)]
    [version(NTDDI_WIN10)]
    interface IXamlPresenterStatics2 : IInspectable
    {
        XamlPresenter Current{ get; };
    }
}
```

### interface Windows.UI.Xaml.Hosting.IXamlPresenterStatics3
```MIDL
namespace Windows.UI.Xaml.Hosting
{
    [exclusiveto(Windows.UI.Xaml.Hosting.XamlPresenter)]
    [uuid(A49DEA01-9E75-49F0-BEEE-EF1592FBC82B)]
    [version(NTDDI_WIN10_RS4)]
    interface IXamlPresenterStatics3 : IInspectable
    {
        XamlPresenter CreateFromCoreWindow(Windows.UI.Core.CoreWindow coreWindow);
    }
}
```
