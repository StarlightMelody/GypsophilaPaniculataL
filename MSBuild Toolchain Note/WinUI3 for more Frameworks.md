# Windows UI 3 for more Frameworks

## Using Windows UI 3 with .NET Built-in WinRT Interop

> [!NOTE]
> - Target:
>     - .NET Framework 4.5 +
>     - .NET Core 3.0 ~ 3.1
> - Dependency: Microsoft.WindowsAppSDK

> [!IMPORTANT]
> From 3.1.0, need [using Windows App SDK with .NET Built-in WinRT Interop](./WinAppSDK%20for%20more%20Frameworks.md#using-windows-app-sdk-by-net-built-in-winrt-interop)

```XML
<PropertyGroup>
  <EnableWin32Codegen>false</EnableWin32Codegen>
</PropertyGroup>
<Target Name="RemoveCSWinRTFlag" BeforeTargets="BeforeBuild">
  <PropertyGroup>
    <_UsingCSWinRT>false</_UsingCSWinRT>
  </PropertyGroup>
  <ItemGroup>
    <XamlFeatureControlFlags Remove="UsingCSWinRT" />
  </ItemGroup>
</Target>
```

### Desktop mode

> [!TIP]
> The *OnLaunched* code in App class which inherit Microsoft.UI.Xaml.Application will determine window environment.
> - Microsoft.UI.Xaml.Window.Current.Activate() -> Windows.UI.Core.CoreWindow -> UWP mode
> - new Microsoft.UI.Xaml.Window().Activate() -> Microsoft.UI.Windowing.AppWindow -> Desktop mode


### UWP Mode

> [!CAUTION]
> Excluding experimental version before 3.1.1, you need enable UWP mode by Registry.
> ```INI
> Windows Registry Editor Version 5.00
>
> [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WinUI\Xaml]
> "EnableUWPWindow"=dword:00000001
> ```


#### Enable Single-project MSIX Packaging

> [!NOTE]
> Need to enable single-project MSIX packaging when using UWP mode.

- ProjectName.csproj
    ```XML
    <PropertyGroup>
      <WindowsAppContainer>true</WindowsAppContainer>
      <EnableMsixTooling>true</EnableMsixTooling>
      <UseLowTrustEntryPoint>true</UseLowTrustEntryPoint>
      <ApplicationEntryPoint>$(RootNamespace).App</ApplicationEntryPoint>
    </PropertyGroup>
    ```

- LaunchSettings.json
    ```JSON
    {
        "profiles": {
            "ProjectName": {
            "commandName": "MsixPackage"
            }
        }
    }
    ```


#### Output AppContainer Executable File

> [!TIP]
> ***Optional***\
> After newer version of Win10, 'AppContainer' flag have no influence to run in UWP mode.

- for .NET Framework

    ```XML
    <PropertyGroup>
      <OutputType>AppContainerExe</OutputType>
      <ImportFrameworkWinFXTargets>false</ImportFrameworkWinFXTargets>
      <AppxPackage>true</AppxPackage>
    </PropertyGroup>
    ```

> [!WARNING]
> Modern .NET Compiler doesn't output an executable program with AppContainer flag(PE header).

- for .NET Core 3

    ```XML
    </PropertyGroup>
      <OutputType>WinExe</OutputType>
    </PropertyGroup>
    ```

> [!TIP]
> You can use EDITBIN(MSVC Tool) to add AppContainer flag.
>
> ```XML
> <Target Name="AddAppContainerPeHeaderFlag">
>   <Exec Command="call &quot;$(DevEnvDir)..\Tools\VsDevCmd.bat&quot; -arch=x64 -host_arch=x64
> EDITBIN.exe /APPCONTAINER:YES &quot;$(TargetPath)&quot;
> EDITBIN.exe /APPCONTAINER:YES &quot;$(RunCommand)&quot;" />
> </Target>
> ```
