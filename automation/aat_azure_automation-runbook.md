Overview
=========

Repetitive activities, or activities not supported by Azure Resource Manager,  are built as runbooks.  In addition to a graphical runbook editor, Azure automation also supports manually written PowerShell and PowerShell workflow runbooks. PowerShell Workflow is a PowerShell extension that allows you to run a PowerShell script on multiple devices in parallel with added functionality such as checkpoints, suspend & restart in the event of failure.  Runbooks are executed as  manually run or scheduled.

Azure Scheduler provides more control over when runbooks run such as on a specific day or in  specific increments. A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it. You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them. When the expiration time is reached, the schedule is disabled

There are 7 different ways in which t a Runbook can be invoked:

| | | | |
|-|-|-|-|
|Azure Portal|	PowerShell|	Webhooks|	Schedule|
|Azure Automation API|	From a Parent Runbook|	Respond to Azure Alert|	


Guidance
=========

Leverage existing PowerShell Modules. PowerShell modules contain cmdlets that you can use in your runbooks, and existing modules that you can install in Azure Automation are available in the PowerShell Gallery. You can launch this gallery from the Azure portal and install them directly into Azure Automation or you can download them and install them manually. 

Consider the different runbook types:

**Powershell Workflow**
|Description|Advantage|Limitations
|-----------|---------|-----------|
|PowerShell Workflow Runbooks are text Runbooks based on PowerShell Workflow. | - Implement all complex logic with PowerShell Workflow code. Use checkpoints to resume Runbook in case of error. <br/> - Use parallel processing to perform multiple actions in parallel.<br/>- Include other Graphical Runbooks and PowerShell Workflow Runbooks as child Runbooks to create high level workflows.| Author must be familiar with PowerShell Workflow. <br/> - Runbook must deal with the additional complexity of PowerShell Workflow such as deserialized objects. <br/>- Runbook takes longer to start than PowerShell Runbooks since it needs to be compiled before running.|

**PowerShell Runbook**
|Description|Advantage|Limitations
|-----------|---------|-----------|
|PowerShell Runbooks are based on PowerShell |- Implement all complex logic with PowerShell code without the additional complexities of PowerShell Workflow. | - Runbook starts faster than Graphical or PowerShell Workflow Runbooks since it doesn't need to be compiled before running.|-Must be familiar with PowerShell scripting. <br/>- Can't use parallel processing to perform multiple actions in parallel. <br> - Can't use checkpoints to resume Runbook in case of error.|

**Graphical Runbook**
|Description|Advantage|Limitations|
|-----------|---------|-----------|
|Graphical Runbooks are created and edited with the graphical editor only in the Azure portal. | -Create Runbooks with minimal knowledge of PowerShell. </br> - Visually represent management processes. </br> - Include other Runbooks as child Runbooks to create high level workflows. </br> - Can be converted to Graphical PowerShell Workflow Runbooks during import and vice-versa. Can be exported to a file and then imported into another automation account.| - Can't edit a Runbook outside of Azure portal.</br> - Can't view or directly edit the PowerShell code that is created by the graphical workflow. </br> - May require additional PowerShell code to perform complex logic. |

**Python Runbook**
|Description|Advantage|Limitations
|-----------|---------|-----------|
|Python runbooks compile under Python 2.| - Utilize the robust standard library of Python.</br> - Must be familiar with Python scripting.| - Only Python 2 is supported at the moment, meaning Python 3 specific functions will fail.|


* The most common methods used to invoke runbooks are:  Schedule, PowerShell, the Azure Portal and Webhooks.
* A parent runbook will often call one or more child runbooks to perform required functionality. 
  * It is a best practice in Azure Automation to write reusable, modular runbooks with a discrete function that can be used by other runbooks.
  * There are limitations using runbooks of different types as a child runbook. See Child runbooks in Azure Automation for more information.
* Activities should reside inside Powershell modules and be as generic as possible and can be consumed by anyone 
* Activities are atomic which implies that any atomic work from runbook perspective should be done in one activity 
* Windows PowerShell provides multiple streams to send output from a script or workflow. Azure Automation works with each of these streams differently. See Runbook output and messages in Azure Automation.
* Runbooks should be managed is source control
* Runbooks should be tested before being published. 
  * Draft versions of  the runbooks execute workflows normally and perform any actions against resources in the environment.
  * Runbooks should only be tested on non-production resources.
  * Azure Automation uses the latest modules in your Automation account when a new scheduled job is run. 
  * To avoid impacting your runbooks and the processes they automate, you should first test any runbooks that have linked schedules with an Automation account dedicated for testing. 
* Use Azure Automation Credentials to allows runbooks to be imported to different automation accounts without changing credentials
* For long running scripts, use checkpoints at important milestones

Preparation
===========
 
* Runbook and module galleries for Azure Automation
* Learning key Windows PowerShell Workflow concepts for Automation runbooks
* Powershell Authoring Best Practices	
* For the Hybrid Runbook Worker to connect to and register with Log Analytics, it must have access to the port number and the URLs that are described in this section. See Plan your network.
	

Procedure:  How to Create and Test an Azure Automation Runbook
===========================================================

1. Create, or import, a runbook
- [Create and import runbooks](https://docs.microsoft.com/en-us/azure/automation/automation-creating-importing-runbook)
- [Create a graphical runbook](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-graphical) 
- [Create a PowerShell runbook ](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-textual-powershell)
- [Create a PowerShell workflow runbook](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-textual) 
- [Create a Python runbook](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-textual-python2)
2. Test a Draft Runbook
- [Test a draft runbook](https://docs.microsoft.com/en-us/azure/automation/automation-testing-runbook)
3. Publish a Runbook
- A runbook must be published before in can be run: [Publishing a runbook](https://docs.microsoft.com/en-us/azure/automation/automation-creating-importing-runbook#publishing-a-runbook)
 
4. Create a webhook
- [Create a webhook](https://docs.microsoft.com/en-us/azure/automation/automation-webhooks#creating-a-webhook)
		
5. Schedule a Runbook
- To [create a new schedule in the Azure portal](https://docs.microsoft.com/en-us/azure/automation/automation-schedules#to-create-a-new-schedule-in-the-azure-portal)
- To [link a schedule to a runbook with Windows PowerShell](https://docs.microsoft.com/en-us/azure/automation/automation-schedules#to-link-a-schedule-to-a-runbook-with-windows-powershell)
	

Next steps
==========
1. Azure Scheduler



