---
title: Windows group
parent: Catalog
---

# UniversalDsc Windows Group

## about_UniversalDsc.Windows/Group

## Short description

The `UniversalDsc.Windows/Group` resource in Microsoft DSC v3 allows you
to manage Windows group accounts.

## Description

The `UniversalDsc.Windows/Group` DSC v3 resource provides a mechanism to manage Windows group
accounts on a system. It handles the lifecycle of group accounts including creation,
configuration, modification, and removal.

With this resource, you can:

- Create new group accounts
- Modify existing group account properties
- Manage group membership by adding or removing users
- Remove group accounts that are no longer needed
- Set group account information such as description and member lists

## Syntax

```powershell
# Get group configuration
$jsonInput = (@{groupName = 'testgroup'} | ConvertTo-Json)
windows-group config get --input $jsonInput

# Set group configuration
$jsonInput = (@{
    groupName = 'newgroup'
    description = 'Test group account'
    members = @('user1', 'user2')
} | ConvertTo-Json)
windows-group config set --input $jsonInput

# Test group configuration
$jsonInput = (@{
    groupName = 'testgroup'
} | ConvertTo-Json)
windows-group config test --input $jsonInput

# Delete group
$jsonInput = (@{
    groupName = 'testgroup'
} | ConvertTo-Json)
windows-group config delete --input $jsonInput

# Export group configuration
windows-group config export
```

## Properties

<!-- markdownlint-disable MD013 -->

| Property    | Description                                                                                                                 | Required |
|-------------|-----------------------------------------------------------------------------------------------------------------------------|----------|
| groupName   | Indicates the group name for the account. This identifier is used for finding the group and should be unique on the system. | Yes      |
| description | Specifies the description of the group account.                                                                             | No       |
| members     | An array of usernames that should be members of this group.                                                                 | No       |
| exist       | Specifies whether the group should exist. Valid values are true or false. Default is true.                                  | No       |

## Exit Codes

The WindowsGroup resource returns the following exit codes:

| Exit Code | Description                   |
| :-------: | ----------------------------- |
|     0     | Success                       |
|     1     | Invalid parameter             |
|     2     | Generic error                 |
|     3     | Invalid JSON                  |
|     4     | Group operation failed        |
|     5     | Access denied                 |

## Examples

### Example 1: Create a new group with description and members

```powershell
$groupConfig = @{
    groupName = "DemoGroup" 
    description = "This group demonstrates the UniversalDsc.Windows/Group resource capabilities"
    members = @("DemoUser", "TestUser")
    exist = $true
}

# Convert the configuration to JSON
$jsonInput = $groupConfig | ConvertTo-Json

# Create the group
windows-group config set --input $jsonInput

# Check if the group was created successfully
windows-group config get --input (@{groupName = "DemoGroup"} | ConvertTo-Json)
```

### Example 2: Test group configuration

```powershell
# Define the group to test
$groupToTest = @{
    groupName = "DemoGroup"
    members = @("DemoUser", "TestUser")
}

# Convert the configuration to JSON
$jsonInput = $groupToTest | ConvertTo-Json

# Test the group configuration
windows-group config test --input $jsonInput
```

### Example 3: Delete a group using JSON input

```powershell
# Define the group to delete
$groupToDelete = @{
    groupName = "DemoGroup"
}

# Convert the configuration to JSON
$jsonInput = $groupToDelete | ConvertTo-Json

# Delete the group
windows-group config delete --input $jsonInput
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
[00]: https://github.com/dscv3-universal-resources/dscv3-universal-resources/blob/main/resources/UniversalDsc.Resource.Windows.Group/README.md
