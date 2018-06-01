Overview 
========

Many things change in the cloud but the accountability around governing, securing,  protecting, monitoring, and configuring remain unchanged. However, new cloud management principles and capabilities have emerged given the scale and pace of change of cloud operations. In this respect the cloud is as much an operating model as it is a technology foundations. 

Azure Automation is one such pervasive capability that fundamentally changes approaches to IT service management. Azure Automation scenarios fall into the following categories:


| |  |  | |
|---------|---------|---------|---------|
|Capacity Management  |  Provisioning       | Monitoring        |  Backup       |
|Compliance    |  Dev / Test Environments       |    Patching	     |   Disaster Recovery      |
|Change Control    |  VM Lifecycle Management       |     Remediation	    |         |



Automation lower costs and improve predictability by enabling IT staff to focus on work that adds business value and reducing error-prone manual activities while lowering costs.

Illustrative  automation examples  include:

		Patch/update/backup 	Change control and 	Monitoring and 
		orchestration	provisioning 	remediation 
		Patch Azure laaS VMs without 	Deploy a VM on Azure/on- 	Alert on a VM then turn on 
		downtime, leveraging Traffic 	premises cloud and enable 	tracing collect logs, upload to 
		Manager.	monitoring for the VM. 	Azure Storage, and make available 
		        		in Visual Studio for 
				troubleshooting. 
				
				See Use an Alert to Trigger a runbook.
				
		Enable regeneration of storage 	Deploy anew service to Azure and 	Monitor for when a new service 
		Account keys while avoiding 	configure the end points for CPU 	gets created and configure it for 
		downtime in the application. 	and memory alerts. 	the right tracing/backup policy. 
		        .
		SQL Backup on a schedule. 	Deploy from Git run 	Notify users of a subscription who 
			validation tests, and swap to 	have underutilized VMS and 
			production if tests pass. 	perform rem ediation. 
		Backup and restore laaS VMs	Monitor SharePoint online for an 	
			to update a service and 
			update the service once


Guidance
========

	• From an operations perspective, the cloud operating model disrupts the traditional ITSM processes. The importance of automation to service operations is well described in  Modern Services Management for Azure Whitepaper.
	
	• Irrespective of tolling, the automation approach should ensure idempotance, immutability, repeatability, testability, and versioning
	• 	Chef	Puppet	Azure Automation DSC
	Client-side	Agent	Agent	Local Configuration Manager
	Azure Install	Chef VM Extension	Puppet VM Extension	DSC VM Extension
	Server-side	Chef Server	Puppet Enterprise Server	Azure Automation DSC Pull Server
	Azure Install	Marketplace VM	Marketplace VM	Azure Automation Account
	Configuration	Cookbook/recipe/run list	Module/class/manifest	Node configuration/DSC resources
	Language	Ruby + Domain Specific	Ruby + Domain Specific	PowerShell
	Dev/test	Kitchen/knife/workstation	Puppet agent –t	LCM/PowerShell ISE
	OS	Windows/Linux++	Windows/Linux ++	Windows ++/Linux
	Community	Supermarket/cookbooks	Forge/modules/curated	PowerShell Gallery/DSC Resources
	

	• The decision to automate, or not automate, should be based on the value over time. This is a question of comparing manual effort to the effort to automate and determining the amount of time it takes to break even.
	• Each customer environment should be evaluated for existing toolsets used for on-premises or public cloud automation. 
		○ Customers may wish to leverage existing expertise and investments in existing toolsets and extend the on-premises functionality to support the automation of Azure constructs.
		○ However, other organizations may wish to have the automation supporting Azure handled separately, without dependencies on legacy or existing platforms. This discovery of each organization’s environment and automation strategy should serve as an input into the overall automation architecture.

	• Hybrid Automation 
		○ Azure Automation cannot access Orchestrator or SMA runbooks. This can be a significant design consideration if an existing investment in automation platforms is required. 
		○ Whether it is self-hosted in Azure or on-premises, these platforms cannot be leveraged for a hybrid automation solution. Typically, Azure Automation would be used in a scenario to deploy or manipulate Azure resources, while additional automation could be used for post-provisioning automation actions when existing automation runbooks already exist for an on-premises resource configuration. Solution designs that require both automation environments should consider the tradeoffs associated with complex or multiple automation solutions. 
		○ For hybrid automation, consider migrating existing Orchestrator runbooks to Azure Automation and using Hybrid Runbook Workers on-premises.
		○ Though System Center Orchestrator can be used as an automation solution for Azure, it is not a preferred solution.  If there has been significant investment in Orchestrator runbooks, consider Migrating them to Azure Automation and use Hybrid Runbook Workers.

Next Steps
==========
	1. Azure Resource Manager
	2. Automation Account
	3. Azure Automation Runbooks
	4. Azure Scheduler

Links
https://azure.microsoft.com/en-us/training/learning-paths/