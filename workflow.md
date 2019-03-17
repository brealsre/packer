## Powershell
### Create a Resource Group
```powershell
$rgName = "mypackerGroup"
$location = "East US"
New-AzResourceGroup -Name $rgName -Location $location
```

### Create a Service Principal
```powershell
$sp = New-AzADServicePrincipal -DisplayName "PackerServicePrincipal"
$BSTR = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($sp.Secret)
$plainPassword = [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($BSTR)
New-AzRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

### Get the Application ID and and Secret Key
```powershell
$plainPassword
$sp.ApplicationId
```

### Get the Subscription Information
```powershell
Get-AzSubscription
```
### Build the Packer Image
./packer build windows.json

## Convert this to Terraform and Azure Secrets Engine for Dynamic Service Prinicpal creation

