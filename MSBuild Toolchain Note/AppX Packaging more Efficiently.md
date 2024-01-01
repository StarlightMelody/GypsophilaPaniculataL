# AppX Packaging more Efficiently

## Embedded Resources
- The URI path of embedded resource is "ms-appx:///" + @(_PackagingOutputsUnexpanded->'%(TargetPath)')
```XML
<ItemGroup>
  <AvailableItemName Include="_PackagingOutputsUnexpanded" />
</ItemGroup>
<ItemGroup>
  <_PackagingOutputsUnexpanded Include="Assets\*">
    <ProjectName>$(ProjectName)</ProjectName>
    <OutputGroup>EmbedOutputGroupForPackaging</OutputGroup>
    <TargetPath>Assets/%(FileName)%(Extension)</TargetPath>
  </_PackagingOutputsUnexpanded>
</ItemGroup>
```
