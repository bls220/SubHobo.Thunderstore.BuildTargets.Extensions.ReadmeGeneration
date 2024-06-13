[![NuGet package](https://img.shields.io/nuget/v/SubHobo.Thunderstore.BuildTargets.Extensions.ReadmeGeneration.svg)](https://nuget.org/packages/SubHobo.Thunderstore.BuildTargets.Extensions.ReadmeGeneration)
[![NuGet downloads](https://img.shields.io/nuget/dt/SubHobo.Thunderstore.BuildTargets.Extensions.ReadmeGeneration.svg)](https://nuget.org/packages/SubHobo.Thunderstore.BuildTargets.Extensions.ReadmeGeneration)
# SubHobo.Thunderstore.BuildTargets.Extensions.ReadmeGeneration
## Overview
This package augments [SubHobo.Thunderstore.BuildTargets](https://nuget.org/packages/SubHobo.Thunderstore.BuildTargets) by addtionally adding generation of the README.md using one or more template files.

Upon building a `README.md` will be generated using [templates specified in your csproj file](#configure).

## Install
Install the SubHobo.Thunderstore.BuildTargets.Extensions.ReadmeGeneration package using the Visual Studio NuGet Package Manager GUI, or the NuGet Package Manager Console:
```
Install-Package SubHobo.Thunderstore.BuildTargets.Extensions.ReadmeGeneration
```
## Configure

### Package Properties
Generation of your package's README.md is as simple as including one or more [template](#templates) files via `ReadmeSection` items in your csproj file. For example, to make a README from a single template:
```xml
<ItemGroup>
    <ReadmeSection Include="_README.md"/>
</ItemGroup>
```

## Templates
README template files are normal markdown files, but they can include properties from your csproj.

Example of basic template file that will pull the title and decription from your project:
```markdown
# $(Title)

$(Description)
```

### Multiple Sections
If you are using multiple templates, place all of your `ReadmeSection`'s in the same `ItemGroup` to ensure the correct ordering.
```xml
<ItemGroup>
    <ReadmeSection Include="Header.md"/>
    <ReadmeSection Include="Body.md"/>
    <ReadmeSection Include="Footer.md"/>
</ItemGroup>
```
### Placeholders
The template files are interpolated by MSBuild, so you can reference any properties/items the same way as in your csproj file.
```xml
$(MyProperty)
@(MyItemCollection)
%(MyItems.Metadata)
```
In the event you want a literal string that matches one of those formats in your README, you can url encode the leading symbol, i.e: `%24(NotAProperty)`

## Example
#### MyProject.csproj
```xml
<PropertyGroup>
    ...
    <Title>My Package</Title>
    <Description>This is Awesome!</Description>
    ...
</PropertGroup>
<ItemGroup>
    <ReadmeSection Include="_README.md"/>
</ItemGroup>
```
#### \_README.md
```markdown
# $(Title)

$(Description)
```
#### Resulting README.md
```markdown
# My Package

This is Awesome!
```

## License
This project is licened under [CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1)<img alt="CC" width="1.5rem" style="width:1.5rem!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img alt="BY" height="22px" style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><img alt="NC" height="22px" style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1"><img alt="SA" height="22px" style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1">