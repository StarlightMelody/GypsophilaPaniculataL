# XAML Controls Internal API

## Windows.UI.Xaml.UIElement

### DirectUI.TearoffXamlDCompInteropPrivate

#### IXamlDCompInteropPrivate
- ppVisual(GetDCompVisual) may be the IDCompositionVisual** type
- ppTransform(CreateDCompTranslateTransform) may be the IDCompositionTranslateTransform** type
```MIDL
[local]
[uuid(04D09168-1945-ACDC-ABBA-C1BEE02BF2E8)]
[version(NTDDI_WIN10)]
interface IXamlDCompInteropPrivate : IUnknown
{
    HRESULT GetDCompVisual([out] IUnknown** ppVisual);
    HRESULT GetDCompSharedVisualHandle([out] HANDLE* pSharedVisualHandle);
    HRESULT DiscardDCompVisual();
    HRESULT OpenSharedResource([in] HANDLE handle, [in] REFIID riid, [out, iid_is(riid)] void** resource);
    HRESULT RequestCommit();
    HRESULT CreateDCompTranslateTransform([out] IUnknown** ppTransform);
}
```

#### IXamlDCompInteropPrivate2
- ppTarget(GetDCompTarget) may be the IDCompositionTarget** type
```MIDL
[local]
[uuid(0F5FD197-210A-412B-923A-8372F6442704)]
[version(NTDDI_WIN10_TH2)]
interface IXamlDCompInteropPrivate2 : IXamlDCompInteropPrivate
{
    HRESULT GetDCompTarget([out] IUnknown** ppTarget);
}
```
