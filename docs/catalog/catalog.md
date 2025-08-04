---
nav_order: 2
has_children: true
has_toc: false
permalink: docs/catalog
---

# Catalog

This is a catalog of available Microsoft DSC resources.

## Resources

You can use PowerShell to retrieve the available release packages from
the [dscv3-universal-resources][00] repository:

```powershell
# Get the latest release packages from the GitHub repository
$repoOwner = "dscv3-universal-resources"
$repoName = "dscv3-universal-resources"
$apiUrl = "https://api.github.com/repos/$repoOwner/$repoName/releases"

# Retrieve releases information
$releases = Invoke-RestMethod -Uri $apiUrl -Method Get

# Display available releases
foreach ($release in $releases) {
    Write-Host "Release: $($release.name) - $($release.tag_name)"
    Write-Host "Published: $($release.published_at)"
    
    if ($release.assets.Count -gt 0) {
        Write-Host "Available assets:"
        foreach ($asset in $release.assets) {
            Write-Host "  - $($asset.name): $($asset.browser_download_url)"
        }
    } else {
        Write-Host "No assets available for this release."
    }
    
    Write-Host "--------------------------"
}
```

You can modify this script to filter specific resource types or
download the packages automatically.

## Available resources

<!-- markdownlint-disable MD013 -->

|    Resource Name    |       Description        |                 Build Status                 |
| :-----------------: | :----------------------: | :------------------------------------------: |
| DSC Windows Service | Manages Windows services |            ![Win32service CI][01]            |
|  DSC Windows User   |   Manage Windows users   | ![UniversalDsc Windows User Resource CI][02] |

<!-- Link reference definitions -->
[00]: https://github.com/dscv3-universal-resources/dscv3-universal-resources/releases
[01]: https://github.com/dscv3-universal-resources/dscv3-universal-resources/actions/workflows/ci.win32service.yml/badge.svg?branch=main
[02]: https://github.com/dscv3-universal-resources/dscv3-universal-resources/actions/workflows/ci.universaldsc.resource.windows.user.yml/badge.svg?branch=main
