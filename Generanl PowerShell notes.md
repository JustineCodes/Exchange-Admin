

Helpful links

Where-Object
	https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-5.1

-   Update/Import module 

-   will not update behind a proxy
-   Run the below first, then update

-   $webclient=New-Object System.Net.WebClient
-   $webclient.Proxy.Credentials = \[System.Net.CredentialCache\]::DefaultNetworkCredentials

-   Edit Profile
  - notepad $PROFILE
  - Edit the file 
  -    
	function prompt {
	 $p = Split-Path -leaf -path (Get-Location)
	 "$p> "
	}
  - Save & Close 

-   Calling property
  - (Command -That doesSomething).PropertyNameNeeded


-   You can pull a command into a $Variable and then dot source the information you need.
-   Example

$test = Get-DistributionGroup -Identity

$Test.BypassModerationFromSendersOrMembers

-   This will give you the names of all accounts with this property name in that distro group

-   HostName

-   $env:computername

-   Script location

$PSScriptRoot/NameOfFile.type

-   Connect behind company proxy

Set-ItemProperty -Path 			'HKLM:\\SOFTWARE\\Wow6432Node\\Microsoft\\.NetFramework\\v4.0.30319' -Name 'SchUseStrongCrypto' -Value '1' -Type DWord

Set-ItemProperty -Path 'HKLM:\\SOFTWARE\\Microsoft\\.NetFramework\\v4.0.30319' -Name 'SchUseStrongCrypto' -Value '1' -Type DWord

Local script path Scriptroot

$PSScriptRoot/

Get manager
```
$Manager=(Get-AdUser (Get-aduser $USERIDNAME -properties manager).manager -properties emailaddress).EmailAddress
```

-Filter
```
Get-EXOMailbox -Filter {name -like 'Acosta, J*'}
Get-ADUser -Filter "Name -like 'Last, F*'"

```

[Where-Object](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-5.1)
```
Get-ADUser -Filter * | Where-Object Name -like "Part, Na*"
```