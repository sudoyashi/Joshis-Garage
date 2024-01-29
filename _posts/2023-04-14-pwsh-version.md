---
layout: post
title: "Get Windows Version with Powershell"
author: "Joshua Domingo"
date:   2099-04-14 00:00:00 -1000
tags: it-admin
categories: it
image: /it-admin/getwindowsversion.jpg
---

*Note: I believe I borrowed this code from somewhere but I can't find the original source. Parameters were adapted to our environment and preferences.*

## The issue: wth is 19045

There are MANY ways to get the Windows version of a remote computer...

```
[System.Environment]::OSVersion.Version
19045

(Get-Wmiobject -Class Win32_OperatingSystem).BuildNumber
19045

(Get-CimInstance -Class Win32_OperatingSystem).BuildNumber
19045

(Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion' -Name CurrentBuild).CurrentBuild
19045

(Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion' -Name UBR).UBR
2846
```

The problem is I don't really care about the specific number, I want to get the human-readable name like *Windows 10 22H2!* Again, there are a number of ways to convert these 19045 or 2846 values to the version we want.

## Powershell Script using a Profile

To use this to its full capability, save this as `Get-Build.ps1` in your Powershell profile that loads all of your scripts.

```
function Get-Build {
<#
.SYNOPSIS
Gets the computer's Windows 10 build number and maps it to a version number.
You'll need to update this script if new versions of Windows come out.
.EXAMPLE
Get-Build -ComputerName VM-JoshuaD... normal output
Get-Build VM-JoshuaD... skips param, normal output
Get-Build -ComputerName VM-JoshuaD | FT ... normal output then formats it into a table.
Get-Build VM-JoshuaD, VM-HomeJoshua | FT ... input multiple computers, comma-separated, then output as a table

Many possibilities to use this information or adapt it to your environment
#>

    Param(
        [Parameter(Position = 0, Mandatory = $true, ValueFromPipeline = $true)][string[]]$ComputerName,
        [int]$Timeout,
        [Alias('Parallel')][switch]$Wait,
        [Alias('Silent')][switch]$Quiet,
        [PSCredential]$Credential
    )
    
    $ScriptBlock = {
        $ver = [PSCustomObject]@{
            22621 = 'Windows 11 22H2'
            22000 = 'Windows 11 21H2'
            19045 = 'Windows 10 22H2'
            19044 = 'Windows 10 21H2'
            19043 = 'Windows 10 21H1'
            19042 = 'Windows 10 20H2'
            19041 = 'Windows 10 2004'
            18363 = 'Windows 10 1909'
            18362 = 'Windows 10 1903'
            17763 = 'Windows 10 1809'
            17134 = 'Windows 10 1803'
            16299 = 'Windows 10 1709'
            15063 = 'Windows 10 1703'
            14393 = 'Windows 10 1607'
            10586 = 'Windows 10 1511'
            10240 = 'Windows 10 1507'
        }
        Get-CimInstance -Class Win32_OperatingSystem | select CSName,BuildNumber,OSArchitecture,@{n='Version';e={$ver.($_.BuildNumber)}} 

    }

    Invoke-Command $ComputerName -ScriptBlock $ScriptBlock
}
```

### How to use

Once the above script is loaded, run the following command:
```
Get-Build -Computername VM-JoshuaD

CSName       BuildNumber  OSArchitecture Version
------       -----------  -------------- -------
VM-JOSHUAD   19045        64-bit         Windows 10 22H2
```

If you are not using Powershell profiles, you can still copy and paste the code above into your shell, but you need to do that every time you want to run the function `Get-Build`.

### Quick and Dirty Version (no Powershell Profiles)

For a quick dirty use case, copy the code block below. You will need to put in a computer name if you want to use this remotely, otherwise, delete the `-ComputerName` parameter.

```
<#
Quick and Dirty Version, don't forget to add a computername!
#>

$ver = [PSCustomObject]@{
            22621 = 'Windows 11 22H2'
            22000 = 'Windows 11 21H2'
            19045 = 'Windows 10 22H2'
            19044 = 'Windows 10 21H2'
            19043 = 'Windows 10 21H1'
            19042 = 'Windows 10 20H2'
            19041 = 'Windows 10 2004'
            18363 = 'Windows 10 1909'
            18362 = 'Windows 10 1903'
            17763 = 'Windows 10 1809'
            17134 = 'Windows 10 1803'
            16299 = 'Windows 10 1709'
            15063 = 'Windows 10 1703'
            14393 = 'Windows 10 1607'
            10586 = 'Windows 10 1511'
            10240 = 'Windows 10 1507'
        }

Get-CimInstance -ComputerName computername -Class Win32_OperatingSystem | select BuildNumber,@{n='Version';e={$ver.($_.BuildNumber)}}
```

## Breakdown: How does the code work

A brief breakdown of the code, if you want more information, head to the official documentation on Microsoft to learn more about Powershell functions.

### Declare Get-Build

```
function Get-Build{
```

Start by declaring this will be a function, this way you can recall this command over and over again when loaded from a Powershell profile.

```
 Param(
        [Parameter(Position = 0, Mandatory = $true, ValueFromPipeline = $true)][string[]]$ComputerName,
        [int]$Timeout,
        [Alias('Parallel')][switch]$Wait,
        [Alias('Silent')][switch]$Quiet,
        [PSCredential]$Credential
    )
```

Open with `Param(` and enter the parameters. We are evaluating the pipeline variable `$ComputerName` to see what computer we want to run the code on.

### Make the scriptblock

```
$ScriptBlock = {
        $ver = [PSCustomObject]@{
            22621 = 'Windows 11 22H2'
            22000 = 'Windows 11 21H2'
            19045 = 'Windows 10 22H2'
            19044 = 'Windows 10 21H2'
            19043 = 'Windows 10 21H1'
            19042 = 'Windows 10 20H2'
            19041 = 'Windows 10 2004'
            18363 = 'Windows 10 1909'
            18362 = 'Windows 10 1903'
            17763 = 'Windows 10 1809'
            17134 = 'Windows 10 1803'
            16299 = 'Windows 10 1709'
            15063 = 'Windows 10 1703'
            14393 = 'Windows 10 1607'
            10586 = 'Windows 10 1511'
            10240 = 'Windows 10 1507'
        }
```

Here we declare the script for `Invoke-Command` for the parameter `-ScriptBlock` as `$ScriptBlock`.

Within the script block, we create an array that stores all the values of the Windows versions as key pairs so it's a recognizable Windows version.

### Get-CimInstance

```
Get-CimInstance -Class Win32_OperatingSystem | select BuildNumber,@{n='Version';e={$ver.($_.BuildNumber)}} 
```

Next, we run `Get-CimInstance...` which will dig up the Windows build information for us. Then we `|` pipe the information to select the correct build number, by referencing the `@{...}` [hashtable](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_hash_tables?view=powershell-7.3).

### Close the Script

```
   }
    Invoke-Command $ComputerName -ScriptBlock $ScriptBlock
}
```

Finally, we wrap up the script with the closing `}` curly braces and use `Invoke-Command...` to complete the task using our `$Scriptblock` on `$ComputerName`.

Done!