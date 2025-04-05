# MRT Internal API

## coclass MrtResourceManager
- Implementation: CMrtResourceManager
- Library: MrmCoreR.dll
```MIDL
[uuid(DBCE7E40-7345-439D-B12C-114A11819A09)]
[version(NTDDI_WIN8)]
coclass MrtResourceManager
{
    interface IUnknown;
    interface IMrtResourceManager;
    [version(NTDDI_WINBLUE)] interface IMrtResourceManager2;
    [version(NTDDI_WIN10_RS2)] interface IMrtResourceManager3;
    [version(NTDDI_WIN10_19H1)] interface IMrtResourceManager4;
    [version(NTDDI_WINBLUE)] interface IInspectable;
}
```

### interface IMrtResourceManager
```MIDL
[uuid(130A2F65-2BE7-4309-9A58-A9052FF2B61C)]
[version(NTDDI_WIN8)]
interface IMrtResourceManager : IUnknown
{
    HRESULT Initialize();
    HRESULT InitializeForCurrentApplication();
    HRESULT InitializeForPackage([in, string] LPCWSTR pszPackageFullName);
    HRESULT InitializeForFile([in, string] LPCWSTR pszFilePath);
    HRESULT GetMainResourceMap([in] REFIID riid, [out, iid_is(riid)] void** ppResourceMap);
    HRESULT GetResourceMap([in, string] LPCWSTR  pszPath, [in] REFIID riid, [out, iid_is(riid)] void** ppResourceMap);
    HRESULT GetDefaultContext([in] REFIID riid, [out, iid_is(riid)] void** ppResourceContext);
    HRESULT GetReference([in] REFIID riid, [out, iid_is(riid)] void** ppResourceReferenceHandler);
    HRESULT IsResourceReference([in, string] LPCWSTR pszReference, [out] BOOL* pbIsResourceReference);
}
```

### interface IMrtResourceManager2
```MIDL
[uuid(439DD7C9-0EEB-4715-BAA7-F0877694E616)]
[version(NTDDI_WINBLUE)]
interface IMrtResourceManager2 : IUnknown
{
    HRESULT InitializeForPackageFile([in, string] LPCWSTR pszFile, [in, string] LPCWSTR pszPackageFullName);
    HRESULT TryInitializeForCurrentApplication();
    HRESULT InitializeForInboxApplication([in, string] LPCWSTR pszFile, [in, string] LPCWSTR pszPackageFullName);
}
```

### interface IMrtResourceManager3
```MIDL
[uuid(76FDFEC5-E7DF-473B-891B-02453923B247)]
[version(NTDDI_WIN10_RS2)]
interface IMrtResourceManager3 : IUnknown
{
    HRESULT InitializeForPackageOrBundle([in, string] LPCWSTR pszPackageFullName);
}
```

### interface IMrtResourceManager4
```MIDL
[uuid(B506D088-F6A5-433B-9411-346515563394)]
[version(NTDDI_WIN10_19H1)]
interface IMrtResourceManager4 : IUnknown
{
    HRESULT GetAllIndividualPriFiles([out] IPriFilePathCollection** ppPriFilePathCollection);
}
```

#### interface IPriFilePathCollection
- Implementation: CMPriFilePathCollection
- Library: MrmCoreR.dll
```MIDL
[uuid(99F94871-7E70-4D31-9BF2-74A291F92EB1)]
[version(NTDDI_WIN10_19H1)]
interface IPriFilePathCollection :IUnknown
{
    HRESULT GetAt([in] DWORD index, [out, string] LPWSTR* pszPriFile);
    HRESULT GetCount([out] DWORD* pCount);
}
```
