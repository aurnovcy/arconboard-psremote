# Onboard to Azure Arc-enabled servers with PowerShell Remoting

You can use the PowerShell cmdlet Connect-AzConnectedMachine to download the Connected Machine agent, install the agent, and register the machine with Azure Arc. The cmdlet downloads the Windows agent package (Windows Installer) from the Microsoft Download Center. You use this process to remotely onboard multiple Windows servers to Azure Arc at scale by using PowerShell remoting.

## PowerShell Remoting Script

Run the following script with administrator privileges. Enter the names of the non-Azure machines to onboard within the array and details of the Azure landing zone (Subscription, Resource Group, and Region) to the placeholder variables. You will need to interactively provide Azure credentials once before deployment.

Note the Supported Environment, OS, and Software requirements as outlined on https://docs.microsoft.com/en-us/azure/azure-arc/servers/agent-overview#prerequisites must be met for each listed hybrid machine for successful onboarding.

```
Enable-PSRemoting
Install-Module -Name Az.ConnectedMachine

$Computers = @("INSERT-COMPUTER-NAME-1", "INSERT-COMPUTER-NAME-2")
$Subscription = "INSERT-SUBSCRIPTION-NAME"
$ResourceGroup = "INSERT-RESOURCE-GROUP-NAME"
$Region = "INSERT-REGION-NAME"
$SecureCredentials = Connect-AzAccount

ForEach($Computer in $Computers) 
{
  $Session = New-PSSession -ComputerName $Computer -Credential $SecureCredentials
  Connect-AzConnectedMachine -SubscriptionId $Subscription -ResourceGroupName $ResourceGroup -Name $Computer -Location $Region -PSSession $Session
  Remove-PSSession $Session
}
```
