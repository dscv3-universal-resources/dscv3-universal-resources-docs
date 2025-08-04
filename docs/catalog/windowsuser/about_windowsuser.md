---
title: Windows user
parent: Catalog
---

# UniversalDsc Windows User

## about_UniversalDsc.Windows/User

## Short description

The `UniversalDsc.Windows/User` resource in Microsoft DSC v3 allows you
to manage Windows user accounts.

## Description

The `UniversalDsc.Windows/User` DSC v3 resource provides a mechanism to manage Windows user accounts
on a system. It handles the lifecycle of user accounts including creation,
configuration, modification, and removal.

With this resource, you can:

- Create new user accounts
- Modify existing user account properties
- Manage user account state (enabled, disabled)
- Remove user accounts that are no longer needed
- Set user account information such as full name, description, and password

## Syntax

```powershell
# Get user configuration
$jsonInput = (@{username = 'testuser'} | ConvertTo-Json)
windows-user config get --input $jsonInput

# Set user configuration
$jsonInput = (@{
    username = 'newuser'
    fullName = 'New User'
    description = 'Test user account'
    password = 'Secret@password'
} | ConvertTo-Json)
windows-user config set --input $jsonInput

# Delete user
$jsonInput = (@{
    username = 'testuser'
} | ConvertTo-Json)
windows-user config delete --input $jsonInput

# Export user configuration
windows-user config export
```

## Properties

<!-- markdownlint-disable MD013 -->

| Property    | Description                                                                                                              | Required            |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------- |
| username    | Indicates the username for the account. This identifier is used for finding the user and should be unique on the system. | Yes                 |
| password    | Specifies the password for the user account. Required when creating a new user account.                                  | Yes (for new users) |
| fullName    | Specifies the full name (display name) of the user account.                                                              | No                  |
| description | Specifies the description of the user account.                                                                           | No                  |
| enabled     | Specifies whether the user account is enabled. Valid values are true or false. Default is true.                          | No                  |
| groups      | An array of group names that this user should be a member of.                                                            | No                  |
| exist       | Specifies whether the user should exist. Valid values are true or false. Default is true.                               | No                  |

## Exit Codes

The WindowsUser resource returns the following exit codes:

| Exit Code | Description                                 |
| :-------: | ------------------------------------------- |
|     0     | Success                                     |
|     1     | Invalid parameter                           |
|     2     | Generic error                               |
|     3     | Invalid JSON                                |
|     4     | An error occurred while processing the user |
|     5     | Access denied                               |

## Examples

### Example 1: Create a new user with full name and description

```powershell
$userConfig = @{
    username = "DemoUser" 
    fullName = "Demonstration User"
    password = "P@ssw0rd123"
    description = "This user demonstrates the UniversalDsc.Windows/User resource capabilities"
    enabled = $true
    exist = $true
}

# Convert the configuration to JSON
$jsonInput = $userConfig | ConvertTo-Json

# Create the user
windows-user config set --input $jsonInput

# Check if the user was created successfully
windows-user config get --input (@{username = "DemoUser"} | ConvertTo-Json)
```

### Example 2: Delete a user using JSON input

```powershell
# Define the user to delete
$userToDelete = @{
    username = "DemoUser"
}

# Convert the configuration to JSON
$jsonInput = $userToDelete | ConvertTo-Json

# Delete the user
windows-user config delete --input $jsonInput
```

## Platform support

| Platform | Supported |
| :------: | :-------: |
| Windows  |    ✅     |
|  macOS   |    ❌     |
|  Linux   |    ❌     |

## Package availability

| Source | Availability |
| :----: | :----------: |
| GitHub |      ✅      |
| NuGet  |      ✅      |
| WinGet |      ✅      |

## Additional information

- [README.md][00]

<!-- Link reference definitions -->
[00]: https://github.com/dscv3-universal-resources/dscv3-universal-resources/blob/main/resources/UniversalDsc.Resource.Windows.User/README.md
