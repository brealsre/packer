## Powershell
### Create a Resource Group
$rgName = "mypackerGroup"
$location = "East US"
New-AzResourceGroup -Name $rgName -Location $location

### Create a Service Principal
$sp = New-AzADServicePrincipal -DisplayName "PackerServicePrincipal"
$BSTR = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($sp.Secret)
$plainPassword = [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($BSTR)
New-AzRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId

### Get the Application ID and and Secret Key
$plainPassword
$sp.ApplicationId

### Get the Subscription Information
Get-AzSubscription

### Build the Packer Image
./packer build windows.json

## Convert this to Terraform and Azure Secrets Engine for Dynamic Service Prinicpal creation

