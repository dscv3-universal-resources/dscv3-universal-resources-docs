---
title: Win32Service
parent: Catalog
---

# Win32Service

## about_Win32Service_resource

## Short description

The Win32Service resource in PowerShell DSC allows you
to manage Windows services.

## Description

The `Win32Service` DSC v3 resource provides a mechanism to manage Windows services
on a system. It handles the lifecycle of a service including installation,
configuration, starting, stopping, and removal.

With this resource, you can:

- Create new services
- Change service configuration (startup type, credentials, dependencies)
- Manage service state (running, stopped)
- Remove services that are no longer needed
- Set service display information and description
- Configure service dependencies and timeout values

## Syntax

```powershell
# Get service configuration
$jsonInput = (@{name = 'winrm'} | ConvertTo-Json)
win32service config get --input $jsonInput

# Set service configuration
$jsonInput = (@{
    name = 'myNewService'
    path = 'pathToExe'
} | ConvertTo-Json)
win32service config set --input $jsonInput

# Delete service
$jsonInput = (@{
    name = 'myNewService'
} | ConvertTo-Json)
win32service config delete --input $jsonInput

# Export service configuration
win32service config export
```

## Properties

<!-- markdownlint-disable MD013 -->

| Property     | Description                                                                                                                      | Required               |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| name         | Indicates the service name. This identifier is used for finding the service and should be unique across the system.              | Yes                    |
| path         | Specifies the path to the service executable file. Required when creating a new service.                                         | Yes (for new services) |
| displayName  | Specifies the display name of the service in service management tools. If not specified, the Name value is used.                 | No                     |
| startupType  | Specifies the startup type for the service. Valid values are: Automatic, Disabled, Manual, Boot, or System. Default is Disabled. | No                     |
| username     | Specifies the username for the account under which the service should run.                                                       | No                     |
| password     | Specifies the password for the account under which the service should run.                                                       | No                     |
| description  | Specifies the description of the service.                                                                                        | No                     |
| dependencies | An array of service names that this service depends on.                                                                          | No                     |

## Examples

### Example 1: Create a new service with description

```powershell
$serviceConfig = @{
    name = "MyDemoService" 
    displayName = "My Demonstration Service"
    path = "C:\Program Files\MyApp\MyService.exe"
    description = "This service demonstrates the Win32Service resource capabilities"
    startupType = "Automatic"
}

# Convert the configuration to JSON
$jsonInput = $serviceConfig | ConvertTo-Json

# Create the service
win32service config set --input $jsonInput

# Check if the service was created successfully
win32service config get --input (@{name = "MyDemoService"} | ConvertTo-Json)
```

### Example 2: Delete a service using JSON input

```powershell
# Define the service to delete
$serviceToDelete = @{
    name = "MyDemoService"
}

# Convert the configuration to JSON
$jsonInput = $serviceToDelete | ConvertTo-Json

# Delete the service
win32service config delete --input $jsonInput
```
