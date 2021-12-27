[[Generanl PowerShell notes]]


Create Remote Mailbox (add mailbox)
```
Enable-RemoteMailbox -Identity sdeaver@pcgus.com -Alias sdeaver -RemoteRoutingAddress sdeaver@publicconsultinggroup.mail.onmicrosoft.com
```
Connect to PCG Exchange
```
Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri [http://wtw2itsppap001.pcgus.com/PowerShell/](http://wtw2itsppap001.pcgus.com/PowerShell/) -Authentication Kerberos

Import-PSSession $Session -AllowClobber
```
Find account by SMTP address
```
Get-Recipient email@doamin.com
```
Remove / add / change SMTP address


Remove;
```
Set-RemoteMailbox -Identity SamAccountName@Domain.com -EmailAddresses @{remove="NAME@Domain.com"}
```
Add;
```
Set-RemoteMailbox -Identity SamAccountName@Domain.com -EmailAddresses @{add="NAME@Domain.com"}
```
Set new primary SMTP
```
Set-RemoteMailbox -Identity SamAccountName@Domain.com -PrimarySmtpAddress NAME@Domain.com
```
