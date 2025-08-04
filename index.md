---
nav_order: 1
---

# Home

DSC v3 universal resources are cross-platform DSC resources built
for Microsoft Desired State Configuration (DSC).
Unlike traditional DSC resources tied to PowerShell, DSC v3 supports authoring
resources in the programming language of your choice — including Python, Go,
PowerShell, and more.

This site serves as a reference and showcase for DSC v3 universal resources,
demonstrating how configurations can be build for various configuration tasks
in different languages. The name *universal* is picked because:

1. **Cross-language support:** Traditional DSC resources are written in
   PowerShell, whereas DSC v3 can be authored in any programming language.
2. **Platform-agnostic design:** DSC v3 targets both Windows, MacOS, and Linux,
   so the same resource logic can be used across multiple operating systems —
   making them "universal" across platforms if applicable.
3. **Standardized schema:** All DSC v3 resources follow a common JSON-based
   schema, enabling a universal contract between configuration author and
   resource logic.
4. **Community driven:** Anyone in the community can author and contribute
    new DSC v3 resources in their preferred language.

## Available resources

The following list represents the current available resources in the repository:

- **Win32Service**
  - A rewritten DSC v3 resource in Python, based on the original `Service`
      resource from `PSDesiredStateConfiguration`. It manages Windows services
      declaratively, including new capabilities supported by DSC's v3 engine.
- **Windows user**
  - A DSC v3 resource for managing Windows user accounts. It provides functionality
      to create, modify, and remove user accounts, including setting user properties
      like full name, description, and password. It's written in .NET using OpenDsc's library.
      Rewritten from the original `PsDscResources` PowerShell module.
- **Windows group**
  - A DSC v3 resource for managing Windows group accounts. It provides functionality
      to create, modify, and remove group accounts, including managing group membership
      and setting group properties like description and member lists. Rewritten from the
      original `PsDscResources` PowerShell module.

More resources in additional languages will be added soon. Stay tuned!

## Installing DSC v3 universal resources

DSC v3 universal resources are published as release assets to GitHub.
To easily install packages, you can run the following code snippet in
a PowerShell session by replacing the placeholder values:

```powershell
# Example installing win32service
$uri = 'https://github.com/dscv3-universal-resources/dscv3-universal-resources/releases/download/v0.1.0/win32service-v0.1.0.zip'
$outFile = Join-Path $env:TEMP 'win32service.zip'
Invoke-WebRequest -Uri $uri -OutFile $outFile
Expand-Archive -Path $outFile -DestinationPath (Split-Path (Get-Command dsc.exe).Path -Parent) -Force
```

To get a list of available Microsoft DSC v3 resources, check out the
[catalog](docs/catalog/catalog.md). You can also go to the GitHub
[releases][00] page and download the asset for your platform.

{: .note }
Microsoft DSC should be installed on the machine for this code to work. If you
wanna install `dsc.exe` easily, use `Install-PSResource -Name PSDSC`
and execute `Install-DscExe`.

<!-- Link reference definitions -->
[00]: https://github.com/dscv3-universal-resources/dscv3-universal-resources/releases
