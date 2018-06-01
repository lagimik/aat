Overview
========

Azure Automation supports PowerShell Desired State Configuration (DSC) is a service to consistently deploy, reliably monitor, and automatically update the desired state of all your Azure resources. DSC assumes a common vanilla operating system imagine where configurations can then be layered. With DSC the following example configurations can be accomplished:

| | | |
|-|-|-|
|Install or remove server roles and features| 	Manage registry settings| 	Manage files and directories| 	Start, stop, and manage processes and services| 	  Manage local groups and user accounts|
|Install and manage packages such as .msi and .exe| 	 Manage environment variables |	Run Windows PowerShell scripts |  Fix a configuration that has drifted away from the desired state |Discover the actual configuration state on a given node|


Through monitoring of configurations Powershell DSC provides flexible and continuous deployment options, prevent configuration drift , and helps ensure compliance.


Guidance
========
* Use a base configuration applied to all machines. Layer team, development language, or technology specific configurations to be layer on the base configuration.
* Leverages existing DSC modules available from [PowerShell Gallery](https://docs.microsoft.com/en-us/azure/automation/automation-runbook-gallery#modules-in-powershell-gallery)
* Forward Azure Automation DSC reporting data to Log Analytics to:
  * Get compliance information for managed nodes and individual resources
  * Trigger an email or alert based on compliance status
  * Write advanced queries across your managed nodes
  * Correlate compliance status across Automation accounts
  * Visualize your node compliance history over time
	

Preparation
===========
Understand the high-level DSC flow:
	
1. Import a DSC configuration to Azure Automation 
2. Compile the DSC configuration into node configuration and it's encrypted by Azure Automation 
3. Node configuration is placed in the DSC agent service and is then pulled by cloud or on-premises machines
4. Node configurations or modules are pulled by the DSC on-boarded Azure VM's and the VM's report on their configuration status and compliance back to the service 
5. Azure VMS conform to the desired 

![dsc-architecture.png](dsc-architecture.png)


Procedure:  Manage Configurations with DSC
==========================================
1. Creating a DSC Configuration
- [Creation](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started#creating-a-dsc-configuration),[Import](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started#importing-a-configuration-into-azure-automation), and [Compile](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-compile) a DSC Configuration
2. Onboard Azure VM
- [Onboard Azure virtual machines ](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#azure-virtual-machines) for configuration management.

3. Forward DSC Diagnostics to Log Analytics
- [Setup integration with Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics#set-up-integration-with-log-analytics) to Foreard status data to Log Analytics workspace
4. View DSC Logs
- View DSC logs in [Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics#view-the-dsc-logs)