[[Generanl PowerShell notes]]
[[Exchange Online Notes]]
[[Create Dynamic Distribution Group]]
	

Get Dynamic group members
```
Set Member veriable

$members = Get-DynamicDistributionGroup -Identity <Distro Name>

Get member names

Get-Recipient -resultsize unlimited -RecipientPreviewFilter $members.ldapRecipientFilter
```

Set reply address
```
Set-MailboxAutoReplyConfiguration <UPN> -StartTime "08/06/2020 1:00 PM" \-AutoReplyState Enabled -AutoDeclineFutureRequestsWhenOOF $True -InternalMessage "<Message>" NOTE: accepts <br> for lines
```

Disable auto map
```
Add-MailboxPermission -Identity UPN -User UPN -AccessRights <CurrentRights> -AutoMapping:$false
```

Copy emails shared mailbox
```
Set-Mailbox UPN -MessageCopyForSentAsEnabled $true -MessageCopyForSendOnBehalfEnabled $true
```

Mailbox restore
```
Search for mailbox
	Get-Mailbox -InactiveMailboxOnly OCHDRMTS | FL Name,DistinguishedName,ExchangeGuid,PrimarySmtpAddress

Set variable
	$InactiveMailbox = Get-Mailbox -InactiveMailboxOnly -Identity

Restore mailbox
	New-MailboxRestoreRequest -SourceMailbox $InactiveMailbox.DistinguishedName -TargetMailbox OCHDRMTS -AllowLegacyDNMismatch
```

Remove-TransportRule
```
Get-TransportRule | Where-Object name -like "*NamePart*"
Remove-TransportRule -Identity "NameOfTransportRule"
```

Get mailbox Guid. Often needed when a user has a soft deleted mailbox in the system.
```
Get-Mailbox -Identity <UserPrincipalName> |  Format-List Name,Distinguishedname,Guid
```

Check for soft deleted mailbox
```
Get-Mailbox -Identity <UserPrincipalName> -IncludeInactiveMailbox |  Format-List Name,Distinguishedname,Guid

```

Mail Trace
For messages in the past 10 days
https://docs.microsoft.com/en-us/powershell/module/exchange/get-messagetrace?view=exchange-ps
```
Get-MessageTrace -SenderAddress <UserPrincipalName> -StartDate 12/10/2021 -EndDate 12/20/2021 | Select-Object RecipientAddress,Status
```

