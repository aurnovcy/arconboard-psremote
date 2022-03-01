# Onboard to Azure Arc-enabled servers with PowerShell Remoting

There are two pre-requisites: 

Install-Module -Name Az.ConnectedMachine
Enable PowerShell remoting with Enable-PSRemoting cmdlet. 

Script

`$Computers = @("INSERT-COMPUTER-NAME-1", "INSERT-COMPUTER-NAME-2")
$ResourceGroup = "INSERT-RESOURCE-GROUP-NAME"
$Region = "INSERT-REGION-NAME"
$Subscription = "INSERT-SUBSCRIPTION-NAME"
$SecureCredentials = Connect-AzAccount

ForEach($Computer in $Computers) 
{
  $Session = New-PSSession -ComputerName $Computer -Credential $SecureCredentials
  Connect-AzConnectedMachine -SubscriptionId $Subscription -ResourceGroupName $ResourceGroup -Name $Computer -Location $Region -PSSession $Session
  Remove-PSSession $Session
}`
