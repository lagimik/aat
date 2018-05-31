Azure Quick Start Guide - Automation

April 2, 2018

7:02 AM

 

 
=

Azure Automation
================

 

 

 

 

> **Azure **
>
> **Quick Start Guide**

 

 

> Draft Version 0.1
>
> April 2018

 

 

 

 

 

 

 

 

This Quick Start Guide provides practical advice when planning and implementing Azure Automation.

 

 

>  

 

© 2018 Microsoft Corporation. All rights reserved. Any use or distribution of these materials without express authorization of Microsoft Corp. is strictly prohibited.

 

 

Copyright

Tuesday, December 19, 2017

8:44 AM

 

Draft Version 1.01

 

 

Copyright

The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication. Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.

MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.

Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The descriptions of other companies' products in this document, if any, are provided only as a convenience to you. Any such references should not be considered an endorsement or support by Microsoft. Microsoft cannot guarantee their accuracy, and the products may change over time. Also, the descriptions are intended as brief highlights to aid understanding, rather than as thorough coverage. For authoritative descriptions of these products, please consult their respective manufacturers.

© 2018 Microsoft Corporation. All rights reserved. Any use or distribution of these materials without express authorization of Microsoft Corp. is strictly prohibited.

Microsoft, Azure, Active Directory, Office 365, SharePoint, Windows, Microsoft Intune, Windows PowerShell, Windows Server, and Xbox Live are either registered trademarks of Microsoft Corporation in the United States and/or other countries.

The names of actual companies and products mentioned herein may be the trademarks of their respective owners.

 

 

Change Log

Friday, March 2, 2018

12:51 PM

 

Draft Version 1.00

 

  Date (2018)   Draft Version   Reason                Summary Description
  ------------- --------------- --------------------- -----------------------------
  May 1         1.00            Development version   First version not released.

 

 

>  

Copyright

The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication. Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.

MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.

Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The descriptions of other companies' products in this document, if any, are provided only as a convenience to you. Any such references should not be considered an endorsement or support by Microsoft. Microsoft cannot guarantee their accuracy, and the products may change over time. Also, the descriptions are intended as brief highlights to aid understanding, rather than as thorough coverage. For authoritative descriptions of these products, please consult their respective manufacturers.

© 2018 Microsoft Corporation. All rights reserved. Any use or distribution of these materials without express authorization of Microsoft Corp. is strictly prohibited.

Microsoft, Azure, Active Directory, Office 365, SharePoint, Windows, Microsoft Intune, Windows PowerShell, Windows Server, and Xbox Live are either registered trademarks of Microsoft Corporation in the United States and/or other countries.

The names of actual companies and products mentioned herein may be the trademarks of their respective owners.

 

 

Azure Automation Overview

Wednesday, March 28, 2018

6:18 AM

 

Overview 
=========

 

Many things change in the cloud but the accountability around governing, securing, protecting, monitoring, and configuring remain unchanged. However, new cloud management principles and capabilities have emerged given the scale and pace of change of cloud operations. In this respect the cloud is as much an operating model as it is a technology foundations.

 

Azure Automation is one such pervasive capability that fundamentally changes approaches to IT service management. Azure Automation scenarios fall into the following categories:

 

  Capacity Management   Provisioning              Monitoring    Backup
  --------------------- ------------------------- ------------- -------------------
  Compliance            Dev / Test Environments   Patching      Disaster Recovery
  Change Control        VM Lifecycle Management   Remediation    

 

Automation lower costs and improve predictability by enabling IT staff to focus on work that adds business value and reducing error-prone manual activities while lowering costs.

 

Illustrative automation examples include:

 

+-----------------------+-----------------------+-----------------------+
| Patch/update/backup   | Change control and    | Monitoring and        |
|                       |                       |                       |
| orchestration         | provisioning          | remediation           |
+=======================+=======================+=======================+
| Patch Azure laaS VMs  | Deploy a VM on        | Alert on a VM then    |
| without               | Azure/on-             | turn on               |
|                       |                       |                       |
| downtime, leveraging  | premises cloud and    | tracing collect logs, |
| Traffic               | enable                | upload to             |
|                       |                       |                       |
| Manager.              | monitoring for the    | Azure Storage, and    |
|                       | VM.                   | make available        |
| >                     |                       |                       |
|                       |                       | in Visual Studio for  |
|                       |                       |                       |
|                       |                       | troubleshooting.      |
|                       |                       |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |                       | See [Use an Alert to  |
|                       |                       | Trigger a             |
|                       |                       | runbook](https://docs |
|                       |                       | .microsoft.com/en-us/ |
|                       |                       | azure/automation/auto |
|                       |                       | mation-create-alert-t |
|                       |                       | riggered-runbook).    |
|                       |                       |                       |
|                       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| Enable regeneration   | Deploy anew service   | Monitor for when a    |
| of storage            | to Azure and          | new service           |
|                       |                       |                       |
| Account keys while    | configure the end     | gets created and      |
| avoiding              | points for CPU        | configure it for      |
|                       |                       |                       |
| downtime in the       | and memory alerts.    | the right             |
| application.          |                       | tracing/backup        |
|                       |                       | policy.               |
| > .                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| SQL Backup on a       | Deploy from Git run   | Notify users of a     |
| schedule.             |                       | subscription who      |
|                       | validation tests, and |                       |
|                       | swap to               | have underutilized    |
|                       |                       | VMS and               |
|                       | production if tests   |                       |
|                       | pass.                 | perform rem ediation. |
+-----------------------+-----------------------+-----------------------+
| Backup and restore    | Monitor SharePoint    |                       |
| laaS VMs              | online for an         |                       |
|                       |                       |                       |
|                       | to update a service   |                       |
|                       | and                   |                       |
|                       |                       |                       |
|                       | update the service    |                       |
|                       | once                  |                       |
+-----------------------+-----------------------+-----------------------+

 

 

Guidance
========

 

-   From an operations perspective, the cloud operating model disrupts the traditional ITSM processes. The importance of automation to service operations is well described in [Modern Services Management for Azure Whitepaper](https://azure.microsoft.com/mediahandler/files/resourcefiles/b6ea597e-2ca2-4bfb-9adc-c8d7292bc81a/Modern%20Service%20Management%20for%20Azure%20v1.1.pdf).

>  

-   Irrespective of tolling, the automation approach should ensure idempotance, immutability, repeatability, testability, and versioning

-   

                      **Chef**                    **Puppet**                 **Azure Automation DSC**
  ------------------- --------------------------- -------------------------- ----------------------------------
  **Client-side**     Agent                       Agent                      Local Configuration Manager
  **Azure Install**   Chef VM Extension           Puppet VM Extension        DSC VM Extension
  **Server-side**     Chef Server                 Puppet Enterprise Server   Azure Automation DSC Pull Server
  **Azure Install**   Marketplace VM              Marketplace VM             Azure Automation Account
  **Configuration**   Cookbook/recipe/run list    Module/class/manifest      Node configuration/DSC resources
  **Language**        Ruby + Domain Specific      Ruby + Domain Specific     PowerShell
  **Dev/test**        Kitchen/knife/workstation   Puppet agent --t           LCM/PowerShell ISE
  **OS**              Windows/Linux++             Windows/Linux ++           Windows ++/Linux
  **Community**       Supermarket/cookbooks       Forge/modules/curated      PowerShell Gallery/DSC Resources

>  

 

-   The decision to automate, or not automate, should be based on the value over time. This is a question of comparing manual effort to the effort to automate and determining the amount of time it takes to break even.

-   Each customer environment should be evaluated for existing toolsets used for on-premises or public cloud automation.

    -   Customers may wish to leverage existing expertise and investments in existing toolsets and extend the on-premises functionality to support the automation of Azure constructs.

    -   However, other organizations may wish to have the automation supporting Azure handled separately, without dependencies on legacy or existing platforms. This discovery of each organization's environment and automation strategy should serve as an input into the overall automation architecture.

 

-   Hybrid Automation

    -   Azure Automation cannot access Orchestrator or SMA runbooks. This can be a significant design consideration if an existing investment in automation platforms is required.

    -   Whether it is self-hosted in Azure or on-premises, these platforms cannot be leveraged for a hybrid automation solution. Typically, Azure Automation would be used in a scenario to deploy or manipulate Azure resources, while additional automation could be used for post-provisioning automation actions when existing automation runbooks already exist for an on-premises resource configuration. Solution designs that require both automation environments should consider the tradeoffs associated with complex or multiple automation solutions.

    -   For hybrid automation, consider migrating existing Orchestrator runbooks to Azure Automation and using Hybrid Runbook Workers on-premises.

    -   Though System Center Orchestrator can be used as an automation solution for Azure, it is not a preferred solution. If there has been significant investment in Orchestrator runbooks, consider Migrating them to Azure Automation and use Hybrid Runbook Workers.

 

Next Steps
==========

1.  [Azure Resource Manager](onenote:#Azure%20Resource%20Manager&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={4BAE005A-7859-4F60-BC85-028CB38002BA}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

2.  [Automation Account](onenote:#Automation%20Account&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={F8600445-06A7-463E-B1E7-89B039F5FD6F}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

3.  [Azure Automation Runbooks](onenote:#Azure%20Automation%20Runbooks&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={38BBE3D8-8E37-4C29-B801-72503F0A019D}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

4.  [Azure Scheduler](onenote:#Azure%20Scheduler&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={95DA48EA-5488-4301-8008-3ABB46EEFA30}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

 

Links

<https://azure.microsoft.com/en-us/training/learning-paths/>

 

 

 

 

 

![Machine generated alternative text:
What is required for self service?
Automation must be leveraged
Use the Service Catalog to present services. Autom ate the process to build the environments and deliver the services.
Activate the services in the service catalog
Alluv users to request pre-built solutions on demand
Permit users to create custom built services on demand
Set up role based access control to specific services
Separate ausiness Services from Technical Ser,\'ices
Plan for automation
Automate the activity to build environments
Construct the environment in Azure using automation
Establish the monitoring through automation
Automatically add the change entry record to the log
use automation to prevent drift & implement compliance
Automate low risks service management tasks
Automote os much os possible
QQQQ
Ert8rpr\*
EM CIBton•rs
SeMce
Automation
O
Anytt\*g
Key Point: Aso remove hVdden Vob0/; mote,-VoVs Ond overheod cost ](''/media/image1.png){width="19.25in" height="10.729166666666666in"}

 

Azure Resource Manager

Tuesday, April 24, 2018

9:22 AM

 

Overview
========

 

The Azure Resource Manager (ARM) provides a consistent management layer for the description, deployment, and control of Azure resources. As such, it is an essential building block of the Azure Automation capabilities.

 

ARM acts as a lifecycle container and offers a declarative solution for deployment which guarantees the end-state each time the deployment is executed.

 

+-----------------------------------+-----------------------------------+
| **Concept**                       | **Description**                   |
+===================================+===================================+
| Resource Group                    | Tightly coupled containers of     |
|                                   | multiple resources of similar or  |
|                                   | different types                   |
|                                   |                                   |
|                                   | Lifecycle: deployment, update,    |
|                                   | delete, status                    |
|                                   |                                   |
|                                   | Identity: resources can talk to   |
|                                   | each other                        |
|                                   |                                   |
|                                   | Grouping: Metering, billing,      |
|                                   | quota: applied & rolled up to     |
|                                   | group                             |
|                                   |                                   |
|                                   | Every resource must exist in one  |
|                                   | and only one resource group       |
|                                   |                                   |
|                                   | Resource groups can span regions  |
|                                   |                                   |
|                                   | Tags                              |
+-----------------------------------+-----------------------------------+
| RBAC                              | Allows secure access with         |
|                                   | granular permissions to resources |
|                                   |                                   |
|                                   | Assignable to users, groups or    |
|                                   | service principals                |
|                                   |                                   |
|                                   | Built-in roles make it easy to    |
|                                   | get started                       |
+-----------------------------------+-----------------------------------+
| Azure Templates                   | Ensure Idempotency                |
|                                   |                                   |
|                                   | Simplify Orchestration            |
|                                   |                                   |
|                                   | Simplify Roll-back                |
|                                   |                                   |
|                                   | Provide Cross-Resource            |
|                                   | Configuration and Update Support  |
|                                   |                                   |
|                                   |                                   |
|                                   |                                   |
|                                   | Azure Templates are:              |
|                                   |                                   |
|                                   | Source file, checked-in           |
|                                   |                                   |
|                                   | Specifies resources and           |
|                                   | dependencies (VMs, WebSites, DBs) |
|                                   | and connections (config, LB sets) |
|                                   |                                   |
|                                   | Parametized input/output          |
+-----------------------------------+-----------------------------------+

 

 

 

Guidance

 

-   [Resource Group Guidance](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#guidance)

    -   Define and deploy your infrastructure through the declarative syntax in Resource Manager templates, rather than through imperative commands.

    -   Declarative model for the ARM templates -- use imperative commands for resource management

    -   Define all deployment and configuration steps in the template. You should have no manual steps for setting up your solution.

    -   Run imperative commands to manage your resources, such as to start or stop an app or machine.

    -   Arrange resources with the same lifecycle in a resource group. Use tags for all other organizing of resources.

-   All the resources in your group should share the same lifecycle. You deploy, update, and delete them together. If one resource, such as a database server, needs to exist on a different deployment cycle it should be in another resource group.

-   A resource group can be used to scope access control for administrative actions.

> Leverage [Quickstart](https://github.com/Azure/azure-quickstart-templates) templates
>
>  
>
>  

 

Preparation

-   Understand the [structure and syntax of Azure Resource Manager templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates)

\* *

\* *

 

Procedure: How to create and deploy an ARM Template

 

1.  Create and Deploy an ARM Template

    a.  [Create and deploy your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template)

 

 

 

Next steps

 

1.  [Automation Account](onenote:#Automation%20Account&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={F8600445-06A7-463E-B1E7-89B039F5FD6F}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

2.  [Azure Automation Runbooks](onenote:#Azure%20Automation%20Runbooks&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={38BBE3D8-8E37-4C29-B801-72503F0A019D}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

3.  [Azure Scheduler](onenote:#Azure%20Scheduler&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={95DA48EA-5488-4301-8008-3ABB46EEFA30}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

 

 

 

 

 

 

 

 

 

Azure Automation Account

Wednesday, April 25, 2018

10:28 AM

 

Overview

 

All the automation components such as runbooks, Hybrid Worker Groups, assets and Desired State Configuration configuration are stored in an *Automation Account*. The Automation account provides a security and automation management boundary for Azure Automation. The Automation Account also specifies the Azure subscription to be billed for Automation usage.

 

 

Guidance

-   When scoping and creating automation accounts, be vigilant about selecting a location to ensure that all Automation components are stored in a particular Azure region and consider the limit of 25 accounts per subscription.

-   Segregate duties within your team and grant only the amount of access to users, groups, and applications that they need to perform their jobs.

-   The recommended method is to use an Azure Run As account.

-   To avoid impacting your runbooks and the processes they automate, you should first test any runbooks that have linked schedules with an Automation account dedicated for testing. This validates your scheduled runbooks continue to work correctly and if not, you can further troubleshoot and apply any changes required before migrating the updated runbook version to production.

-   Integrate the Automation Account with source control to enable team collaboration, track changes, roll back to earlier versions, define branches for development, test or production Automation accounts.

 

Preparation

 

 

1.  Ensure you have the appropriate permission to define the Automation Account

    a.  [Required permissions to update your Automation account ](https://docs.microsoft.com/en-us/azure/automation/automation-create-runas-account)

<!-- -->

1.  Understand the role-based access of the Automation Account

    a.  [Role-based access control in Azure Automation ](https://docs.microsoft.com/en-us/azure/automation/automation-role-based-access-control)

 

 

Procedure: How to Create an Azure Automation Account

 

1.  Create Azure Automation Account and RunAs Account

    a.  [Create an Azure Automation account](https://docs.microsoft.com/en-us/azure/automation/automation-quickstart-create-account#create-automation-account)

<!-- -->

1.  Control targeting of automation

    a.  [Limiting Run As account permissions ](https://docs.microsoft.com/en-us/azure/automation/automation-create-runas-account#limiting-run-as-account-permissions)

<!-- -->

1.  Test Azure Automation Run As account authentication

    a.  [Verify RunAs Authentication](https://docs.microsoft.com/en-us/azure/automation/automation-verify-runas-authentication)

<!-- -->

1.  Enable Monitoring

    a.  [Forward job status and job streams from Automation to Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics%3e)

<!-- -->

1.  Source Control

    a.  [Set up source control in Azure Automation](https://docs.microsoft.com/en-us/azure/automation/automation-source-control-integration)

 

 

Next steps

 

1.  [Azure Automation Runbooks](onenote:#Azure%20Automation%20Runbooks&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={38BBE3D8-8E37-4C29-B801-72503F0A019D}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

2.  [Azure Scheduler](onenote:#Azure%20Scheduler&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={95DA48EA-5488-4301-8008-3ABB46EEFA30}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

 

Azure Automation Assets

Monday, April 30, 2018

1:22 PM

 

Overview
========

 

Azure Automation Assets are resources (also called "settings") that are globally available to be used in or associated with a runbook.

 

+-----------------------------------+-----------------------------------+
| Asset                             | Use                               |
+===================================+===================================+
| Schedules                         | Azure Automation Schedules are    |
|                                   | used to schedule runbooks to run  |
|                                   | automatically. This could be      |
|                                   | either a single date and time for |
|                                   | the runbook to run once, or it    |
|                                   | could be a recurring schedule to  |
|                                   | start the runbook multiple times  |
+-----------------------------------+-----------------------------------+
| Integration Modules               | An integration module is a        |
|                                   | package that contains a Windows   |
|                                   | PowerShell Module and can be      |
|                                   | imported into Azure Automation.   |
|                                   | Imported modules are distributed  |
|                                   | to all Azure Automation worker    |
|                                   | servers so that they are          |
|                                   | available to runbooks.            |
+-----------------------------------+-----------------------------------+
| Connections                       | Connections define the            |
|                                   | information required to connect   |
|                                   | to a service or application from  |
|                                   | a runbook. The different types of |
|                                   | connections are defined by the    |
|                                   | integration modules imported into |
|                                   | Automation, and typically include |
|                                   | such information credentials the  |
|                                   | host or service URI to connect    |
|                                   | to. This information can then be  |
|                                   | passed as one or more parameters  |
|                                   | to the integration modules        |
|                                   | activities, to make required      |
|                                   | connections.                      |
+-----------------------------------+-----------------------------------+
| Variables                         | Variables are values that are     |
|                                   | available to all runbooks. They   |
|                                   | can be created, modified, and     |
|                                   | retrieved from the Azure Portal,  |
|                                   | Windows PowerShell, or from       |
|                                   | within a runbook.                 |
|                                   |                                   |
|                                   | They can be used in runbooks to   |
|                                   | define frequently-used settings,  |
|                                   | such as directory paths to common |
|                                   | files, server names, or other     |
|                                   | strings.                          |
|                                   |                                   |
|                                   | Variable settings store *string,  |
|                                   | boolean, integer, or datetime*    |
|                                   | information that can then be used |
|                                   | in a runbook. They can also       |
|                                   | contain complex objects (stored   |
|                                   | as property bags).                |
+-----------------------------------+-----------------------------------+
| Credentials and Certificates      | Credentials are either a username |
|                                   | and password combination that can |
|                                   | be used with Windows PowerShell   |
|                                   | commands or a certificate that is |
|                                   | uploaded to Azure Automation. The |
|                                   | properties for a credential are   |
|                                   | stored securely in Automation,    |
|                                   | and can be accessed in the        |
|                                   | runbook with either the           |
|                                   | Get-AutomationPSCredential or     |
|                                   | Get-AutomationCertificate         |
|                                   | activity.                         |
+-----------------------------------+-----------------------------------+

 

 

 

Guidance
========

-   Variables are created to:

    -   Share a value between multiple runbooks.

    -   Share a value between multiple jobs from the same runbook.

    -   Manage a value from the Azure Portal or from the Windows PowerShell command line that is used by runbooks

-   Azure Automation created Connection type asset to:

    -   Group the connection data necessary to connect to an external system into a single object so that it can be accessed by runbooks easily

    -   Provide a template describing how a connection for a certain system should look like so that users can use this template when defining the connection to this system

    -   Changes to the connection data can be made in a single place without having to replicate the change in multiple locations (variable assets, runbooks, etc)

-   Use Azure Automation credentials as a unified and secure way to store and reference credentials in runbooks.

-   Leverages existing integration modules available from [PowerShell Gallery](https://docs.microsoft.com/en-us/azure/automation/automation-runbook-gallery#modules-in-powershell-gallery)

-   When creating modules, apply Azure Automation Integration Module [authoring Best Practices](https://docs.microsoft.com/en-us/azure/automation/automation-integration-modules#authoring-best-practices).

 

 

Preparation

\* *

 

 

Procedure:

 

1.  Create new Automation Variable

    a.  [Define automation varibles](https://docs.microsoft.com/en-us/azure/automation/automation-variables#creating-a-new-automation-variable) to be used in runbooks.

<!-- -->

1.  Creating a New Connection

    a.  [Define connections](https://docs.microsoft.com/en-us/azure/automation/automation-connections#creating-a-new-connection) to be used in runbooks.

<!-- -->

1.  Create a New Schedule

    a.  [Create a schedule](https://docs.microsoft.com/en-us/azure/automation/automation-schedules#creating-a-schedule) to invoke runbooks.

<!-- -->

1.  Create a New Credential

    a.  Create and securely store [automation credentials](https://docs.microsoft.com/en-us/azure/automation/automation-credentials#creating-a-new-credential-asset).

<!-- -->

1.  Creating a New Certificate

    a.  [Create certificates](https://docs.microsoft.com/en-us/azure/automation/automation-certificates)

>  

 

Next steps

1.  [Azure Automation Runbooks ](onenote:#Azure%20Automation%20Runbooks%20&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={38BBE3D8-8E37-4C29-B801-72503F0A019D}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

 

Azure Automation Runbooks

Monday, April 23, 2018

11:01 AM

 

Overview
========

 

Repetitive activities, or activities not supported by Azure Resource Manager, are built as runbooks. In addition to a graphical runbook editor, Azure automation also supports manually written PowerShell and PowerShell workflow runbooks. PowerShell Workflow is a PowerShell extension that allows you to run a PowerShell script on multiple devices in parallel with added functionality such as checkpoints, suspend & restart in the event of failure. Runbooks are executed as manually run or scheduled.

 

Azure Scheduler provides more control over when runbooks run such as on a specific day or in specific increments. A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it. You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them. When the expiration time is reached, the schedule is disabled

 

There are 7 different ways in which t a Runbook can be invoked:

 

  Azure Portal           PowerShell              Webhooks                 Schedule
  ---------------------- ----------------------- ------------------------ ----------
  Azure Automation API   From a Parent Runbook   Respond to Azure Alert    

 

 

 

Guidance
========

 

Leverage existing PowerShell Modules. PowerShell modules contain cmdlets that you can use in your runbooks, and existing modules that you can install in Azure Automation are available in the [PowerShell Gallery](http://www.powershellgallery.com/). You can launch this gallery from the Azure portal and install them directly into Azure Automation or you can download them and install them manually.

 

Consider the different runbook types:

 

+-----------------+-----------------+-----------------+-----------------+
| Type            | Description     | Advantages      | Limitations     |
+=================+=================+=================+=================+
| PowerShell      | PowerShell      | Implement all   | Author must be  |
| Workflow        | Workflow        | complex logic   | familiar with   |
| Runbooks        | Runbooks are    | with PowerShell | *PowerShell     |
|                 | text Runbooks   | Workflow code.  | Workflow*.      |
|                 | based on        |                 |                 |
|                 | *PowerShell     |                 |                 |
|                 | Workflow*.      |                 |                 |
|                 |                 | Use checkpoints | Runbook must    |
|                 |                 | to resume       | deal with the   |
|                 |                 | Runbook in case | additional      |
|                 |                 | of error.       | complexity of   |
|                 |                 |                 | PowerShell      |
|                 |                 |                 | Workflow such   |
|                 |                 |                 | as deserialized |
|                 |                 | Use parallel    | objects.        |
|                 |                 | processing to   |                 |
|                 |                 | perform         |                 |
|                 |                 | multiple        |                 |
|                 |                 | actions in      | Runbook takes   |
|                 |                 | parallel.       | longer to start |
|                 |                 |                 | than PowerShell |
|                 |                 |                 | Runbooks since  |
|                 |                 |                 | it needs to be  |
|                 |                 | Include other   | compiled before |
|                 |                 | Graphical       | running.        |
|                 |                 | Runbooks and    |                 |
|                 |                 | PowerShell      |                 |
|                 |                 | Workflow        |                 |
|                 |                 | Runbooks as     |                 |
|                 |                 | child Runbooks  |                 |
|                 |                 | to create high  |                 |
|                 |                 | level           |                 |
|                 |                 | workflows.      |                 |
+-----------------+-----------------+-----------------+-----------------+
| PowerShell      | PowerShell      | Implement all   | Must be         |
| Runbook         | Runbooks are    | complex logic   | familiar with   |
|                 | based on        | with PowerShell | *PowerShell*    |
|                 | *PowerShell*.   | code without    | scripting.      |
|                 |                 | the additional  |                 |
|                 |                 | complexities of |                 |
|                 |                 | PowerShell      |                 |
|                 |                 | Workflow.       | Can\'t use      |
|                 |                 |                 | parallel        |
|                 |                 |                 | processing to   |
|                 |                 |                 | perform         |
|                 |                 | Runbook starts  | multiple        |
|                 |                 | faster than     | actions in      |
|                 |                 | Graphical or    | parallel.       |
|                 |                 | PowerShell      |                 |
|                 |                 | Workflow        | Can\'t use      |
|                 |                 | Runbooks since  | checkpoints to  |
|                 |                 | it doesn\'t     | resume Runbook  |
|                 |                 | need to be      | in case of      |
|                 |                 | compiled before | error.          |
|                 |                 | running.        |                 |
+-----------------+-----------------+-----------------+-----------------+
| Graphical       | Graphical       | Create Runbooks | Can\'t edit a   |
| Runbook         | Runbooks are    | with minimal    | Runbook outside |
|                 | created and     | knowledge of    | of Azure        |
|                 | edited with the | PowerShell.     | portal.         |
|                 | graphical       |                 |                 |
|                 | editor only in  |                 |                 |
|                 | the *Azure      |                 |                 |
|                 | portal*.        | Visually        | Can\'t view or  |
|                 |                 | represent       | directly edit   |
|                 | >               | management      | the PowerShell  |
|                 |                 | processes.      | code that is    |
|                 |                 |                 | created by the  |
|                 |                 | Include other   | graphical       |
|                 |                 | Runbooks as     | workflow.       |
|                 |                 | child Runbooks  |                 |
|                 |                 | to create high  |                 |
|                 |                 | level           |                 |
|                 |                 | workflows.      | May require     |
|                 |                 |                 | additional      |
|                 |                 |                 | PowerShell code |
|                 |                 |                 | to perform      |
|                 |                 | Can be          | complex logic.  |
|                 |                 | converted to    |                 |
|                 |                 | Graphical       |                 |
|                 |                 | PowerShell      |                 |
|                 |                 | Workflow        |                 |
|                 |                 | Runbooks during |                 |
|                 |                 | import and      |                 |
|                 |                 | vice-versa. Can |                 |
|                 |                 | be exported to  |                 |
|                 |                 | a file and then |                 |
|                 |                 | imported into   |                 |
|                 |                 | another         |                 |
|                 |                 | automation      |                 |
|                 |                 | account.        |                 |
+-----------------+-----------------+-----------------+-----------------+
| Python Runbook  | Python runbooks | Utilize the     | Must be         |
|                 | compile under   | robust standard | familiar with   |
|                 | Python 2.       | library of      | Python          |
|                 |                 | Python.         | scripting.      |
|                 |                 |                 |                 |
|                 |                 |                 |                 |
|                 | \* *            |                 |                 |
|                 |                 |                 | Only Python 2   |
|                 |                 |                 | is supported at |
|                 |                 |                 | the moment,     |
|                 |                 |                 | meaning Python  |
|                 |                 |                 | 3 specific      |
|                 |                 |                 | functions will  |
|                 |                 |                 | fail.           |
+-----------------+-----------------+-----------------+-----------------+

 

-   The most common methods used to invoke runbooks are: *Schedule, PowerShell, the Azure Portal and Webhooks*.

-   A parent runbook will often call one or more child runbooks to perform required functionality.

    -   It is a best practice in Azure Automation to write reusable, modular runbooks with a discrete function that can be used by other runbooks.

    -   There are limitations using runbooks of different types as a child runbook. See [Child runbooks in Azure Automation](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/automation/automation-child-runbooks.md) for more information.

>  

-   Activities should reside inside Powershell modules and be as generic as possible and can be consumed by anyone 

-   Activities are atomic which implies that any atomic work from runbook perspective should be done in one activity 

-   Windows PowerShell provides [multiple streams](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) to send output from a script or workflow. Azure Automation works with each of these streams differently. See [Runbook output and messages in Azure Automation](https://docs.microsoft.com/en-us/azure/automation/automation-runbook-output-and-messages).

<!-- -->

-   Runbooks should be managed is source control

-   Runbooks should be tested before being published.

    -   Draft versions of the runbooks execute workflows normally and perform any actions against resources in the environment.

    -   Runbooks should only be tested on non-production resources.

    -   Azure Automation uses the latest modules in your Automation account when a new scheduled job is run.

    -   To avoid impacting your runbooks and the processes they automate, you should first test any runbooks that have linked schedules with an Automation account dedicated for testing.

-   Use Azure Automation Credentials to allows runbooks to be imported to different automation accounts without changing credentials

-   For long running scripts, use checkpoints at important milestones

 

 

 

Preparation

-   [Runbook and module galleries](https://docs.microsoft.com/en-us/azure/automation/automation-runbook-gallery) for Azure Automation

-   Learning [key Windows PowerShell Workflow concepts](https://docs.microsoft.com/en-us/azure/automation/automation-powershell-workflow) for Automation runbooks

-   [Powershell Authoring Best Practices](onenote:#Powershell%20Authoring%20Best%20Practices&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={3F4BFB3B-725B-4D0A-9CCE-5BED0C67DA37}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

>  
>
> For the Hybrid Runbook Worker to connect to and register with Log Analytics, it must have access to the port number and the URLs that are described in this section. See [Plan your network](https://docs.microsoft.com/en-us/azure/automation/automation-offering-get-started#network-planning).
>
>  

\* *

 

Procedure: How to Create and Test an Azure Automation Runbook

###  

1.  Create, or import, a runbook

    a.  [Create and import runbooks ](https://docs.microsoft.com/en-us/azure/automation/automation-creating-importing-runbook)

    b.  [Create a graphical runbook ](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-graphical)

    c.  [Create a PowerShell runbook ](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-textual-powershell)

    d.  [Create a PowerShell workflow runbook ](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-textual)

    e.  [Create a Python runbook](https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-textual-python2)

>  

1.  Test a Draft Runbook

    a.  [Test a draft runbook](https://docs.microsoft.com/en-us/azure/automation/automation-testing-runbook)

>  

1.  Publish a Runbook

    a.  A runbook must be published before in can be run: [Publishing a runbook](https://docs.microsoft.com/en-us/azure/automation/automation-creating-importing-runbook#publishing-a-runbook)

>  

1.  Create a webhook

    a.  [Create a webhook](https://docs.microsoft.com/en-us/azure/automation/automation-webhooks#creating-a-webhook)

>  

1.  Schedule a Runbook

    a.  [To create a new schedule in the Azure portal](https://docs.microsoft.com/en-us/azure/automation/automation-schedules#to-create-a-new-schedule-in-the-azure-portal)

    b.  [To link a schedule to a runbook with Windows PowerShell](https://docs.microsoft.com/en-us/azure/automation/automation-schedules#to-link-a-schedule-to-a-runbook-with-windows-powershell)

>  

 

Next steps

1.  [Azure Scheduler](onenote:#Azure%20Scheduler&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={95DA48EA-5488-4301-8008-3ABB46EEFA30}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

 

 

 

 

Azure Scheduler

Tuesday, April 24, 2018

9:22 AM

 

Overview
========

 

Azure Scheduler is a service for scheduling reliable actions on a recurrent or calendar aware-basis, executed reliably even in the face of network, machine, and data center failures. Scheduler can invoke actions---such as calling HTTP/S endpoints or posting a message to a storage queue on any schedule. Scheduler can schedule jobs to call services both inside and outside of Azure and run those jobs on demand, on a regularly recurring schedule, or designate them for a future date.

 

 

+-----------------------------------+-----------------------------------+
| Resource                          | Description                       |
+===================================+===================================+
| **Job collection**                | A job collection contains a group |
|                                   | of jobs and maintains settings,   |
|                                   | quotas, and throttles that are    |
|                                   | shared by jobs within the         |
|                                   | collection. A job collection is   |
|                                   | created by a subscription owner   |
|                                   | and groups jobs together based on |
|                                   | usage or application boundaries.  |
|                                   | It's constrained to one region.   |
|                                   | It also allows the enforcement of |
|                                   | quotas to constrain the usage of  |
|                                   | all jobs in that collection. The  |
|                                   | quotas include MaxJobs and        |
|                                   | MaxRecurrence.                    |
+-----------------------------------+-----------------------------------+
| **Job**                           | A job defines a single recurrent  |
|                                   | action, with simple or complex    |
|                                   | strategies for execution. Actions |
|                                   | may include HTTP, storage queue,  |
|                                   | service bus queue, or service bus |
|                                   | topic requests.                   |
+-----------------------------------+-----------------------------------+
| **Job history**                   | A job history represents details  |
|                                   | for an execution of a job. It     |
|                                   | contains success vs. failure, as  |
|                                   | well as any response details.     |
|                                   |                                   |
|                                   |                                   |
+-----------------------------------+-----------------------------------+

 

Schedules for many behavior patterns, including:

-   Run once at a specific date and time.

-   Run and recur a specific number of times.

-   Run immediately and recur.

-   Run and recur every *n* minutes, hours, days, weeks, or months, starting at a specific time.

-   Run and recur at a weekly or monthly frequency, but only on specific days of the week or on specific days of the month.

-   Run and recur multiple times in a period. For example, on the last Friday and last Monday of every month, or at 5:15 AM and at

 

 
=

Guidance
========

  Job Type                                            Usage
  --------------------------------------------------- -----------------------------------------------------------------------------------------------------------
  HTTP jobs (including HTTPS jobs that support SSL)   HTTP jobs used against existing endpoints for a workload or service
  storage queue jobs                                  Storage queue jobs can be used to to post messages to storage queues for workloads that use storage queue
  service bus queue and topic jobs                    Service bus jobs are ideal for workloads that use service bus queues and topics.

 

Included your scheduled jobs as part of the workload deployment

 

 

Preparation
===========

 

-   Understand the Azure Scheduler [Job Schema Basic](https://docs.microsoft.com/en-in/azure/scheduler/scheduler-advanced-complexity#job-schema-basics), and key fields [StartTime](https://docs.microsoft.com/en-in/azure/scheduler/scheduler-advanced-complexity#deep-dive-starttime), [Schedule](https://docs.microsoft.com/en-in/azure/scheduler/scheduler-advanced-complexity#deep-dive-schedule), [Recurring Schedules](https://docs.microsoft.com/en-in/azure/scheduler/scheduler-advanced-complexity#examples-recurrence-schedules) and deep dive into some [limits and examples](https://docs.microsoft.com/en-in/azure/scheduler/scheduler-advanced-complexity#job-schema-defaults-limits-and-examples).

-   Review the [Scheduler Job with Web App](https://github.com/Azure/azure-quickstart-templates/tree/052db5feeba11f85d57f170d8202123511f72044/201-scheduler-webapp) Quickstart template.

 

 
=

Procedure: How to Create a Job
==============================

 

1.  Create a Job

    a.  Use the Azure portal to [create a job](onenote:#section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation%20(TOC).one)

    b.  Use JSON and the REST API to [create a schedule](https://docs.microsoft.com/en-in/azure/scheduler/scheduler-advanced-complexity#use-json-and-the-rest-api-to-create-a-schedule)

<!-- -->

1.  Manage and Monitor Jobs

    a.  <https://docs.microsoft.com/en-in/azure/scheduler/scheduler-get-started-portal#manage-and-monitor-jobs>

>  

Next steps
==========

1.  [Azure Desired State Configuration (DSC)](onenote:#Azure%20Desired%20State%20Configuration%20(DSC)&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={769D385B-444F-415D-88B7-C6EC38037756}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation.one)

2.  [Azure Data Factory Pipeline](onenote:#Azure%20Data%20Factory%20Pipeline&section-id={6D516662-CAC6-4019-8463-9AF6FD020AE7}&page-id={E20018DC-100E-4E16-9C8C-EEE7ED4F2FA1}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Azure%20Automation.one)

 

 

Automation for VM Lifecycle Management

Monday, April 30, 2018

3:05 PM

 

Azure Desired State Configuration (DSC)

Tuesday, April 24, 2018

9:23 AM

 

Overview
========

 

Azure Automation supports PowerShell Desired State Configuration (DSC) is a service to consistently deploy, reliably monitor, and automatically update the desired state of all your Azure resources. DSC assumes a common vanilla operating system imagine where configurations can then be layered. With DSC the following example configurations can be accomplished:

 

  Install or remove server roles and features         Manage registry settings       Manage files and directories     Start, stop, and manage processes and services                         Manage local groups and user accounts
  --------------------------------------------------- ------------------------------ -------------------------------- -------------------------------------------------------------------- ---------------------------------------------------------
  Install and manage packages such as .msi and .exe   Manage environment variables   Run Windows PowerShell scripts     Fix a configuration that has drifted away from the desired state   Discover the actual configuration state on a given node

 

 

Through monitoring of configurations Powershell DSC provides flexible and continuous deployment options, prevent configuration drift , and helps ensure compliance.

 

 

Guidance

-   Use a base configuration applied to all machines. Layer team, development language, or technology specific configurations to be layer on the base configuration.

-   Leverages existing DSC modules available from [PowerShell Gallery](https://docs.microsoft.com/en-us/azure/automation/automation-runbook-gallery#modules-in-powershell-gallery)

-   [Forward Azure Automation DSC reporting data to Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics) to:

    -   Get compliance information for managed nodes and individual resources

    -   Trigger an email or alert based on compliance status

    -   Write advanced queries across your managed nodes

    -   Correlate compliance status across Automation accounts

    -   Visualize your node compliance history over time

>  

 

Preparation

> Understand the high-level DSC flow:
>
>  

1.  Import a *DSC configuration* to Azure Automation

2.  Compile the DSC configuration into *node configuration* and it\'s encrypted by Azure Automation

3.  Node configuration is placed in the DSC agent service and is then pulled by cloud or on-premises machines

4.  Node configurations or modules are pulled by the DSC on-boarded Azure VM\'s and the VM\'s report on their configuration status and compliance back to the service

5.  Azure VMS conform to the desired

 

![Azure Portal
Pcnv«SheII
DSC API
System
Doimd State
Machines configured
to receive DSC
Azure Virtual
Azure
Enterprise
An imparts DSC
ccnfgurato-, to Azure Automation
An actcr compiles the DSC
it\'S
Azure Automaton
configuration is in
the DSC agent is then
Oy cloud or on-premises
machines
Cloud --- Node confguration5 or
DSC on-
b:arded Azure VMS and the VMS
report on their configuraticn status
and cc•mOiance back to the se%\'ice
Azure VMS conform to the desired
On•premises --- node configuration is
pulLed on to local macnne
configured to receive DSC,
Orppremises machines must have
etner Windows Management
Framework S installed f a
the Linu\* Agent
installed for a Linux node. Tncse
machines act cn local resources as
conform to
desired state ](''/media/image2.png){width="10.0in" height="6.979166666666667in"}

 

 

Procedure: Manage Configurations with DSC

 

1.  Creating a DSC Configuration

    a.  <https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started#creating-a-dsc-configuration>

<!-- -->

1.  Important a Configuration

    a.  <https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started#importing-a-configuration-into-azure-automation>

<!-- -->

1.  Compile DSC Configuration

    a.  <https://docs.microsoft.com/en-us/azure/automation/automation-dsc-compile>

<!-- -->

1.  Onboard Azure VM

    a.  <https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#azure-virtual-machines>

<!-- -->

1.  View DSC Logs

    a.  View [DSC logs in Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics#view-the-dsc-logs)

 

 

 

Automation for Data Management

Wednesday, March 28, 2018

6:19 AM

 

Azure Data Factory Pipeline

Monday, April 30, 2018

1:57 PM

 

Overview
========

 

Azure Data Factory is a cloud-based data integration service to create data-driven workflows to orchestrating and automating data movement and data transformation. Data Factory uses data-driven workflows to orchestrate movement of data between supported data stores. Note that Azure Data Factory does not store any data except for linked service credentials for cloud data stores, which are encrypted by using certificates.

 

Azure Data Factory consists of the following concepts:

 

![DATA SET
i data
UNKED SERVICE ](''/media/image3.png){width="12.458333333333334in" height="3.9375in"}

 

 

+-----------------------------------+-----------------------------------+
| Concept                           | Description                       |
+===================================+===================================+
| [Pipeline](https://docs.microsoft | A data factory might have one or  |
| .com/en-us/azure/data-factory/int | more pipelines. A pipeline is a   |
| roduction#pipeline)               | logical grouping of activities    |
|                                   | that performs a unit of work.     |
|                                   | Together, the activities in a     |
|                                   | pipeline perform a task. A        |
|                                   | [Pipeline                         |
|                                   | Run](https://docs.microsoft.com/e |
|                                   | n-us/azure/data-factory/introduct |
|                                   | ion#pipeline-runs)                |
|                                   | is an instance of the pipeline    |
|                                   | execution.                        |
|                                   | [Parameters](https://docs.microso |
|                                   | ft.com/en-us/azure/data-factory/i |
|                                   | ntroduction#parameters)           |
|                                   | are key-value pairs of read-only  |
|                                   | configuration.                    |
+-----------------------------------+-----------------------------------+
| [Activity](https://docs.microsoft | Activities represent a processing |
| .com/en-us/azure/data-factory/int | step in a pipeline.               |
| roduction#activity)               |                                   |
|                                   | Data Factory supports three types |
|                                   | of activities: data movement      |
|                                   | activities, data transformation   |
|                                   | activities, and control           |
|                                   | activities.                       |
+-----------------------------------+-----------------------------------+
| [Datasets](https://docs.microsoft | Datasets represent data           |
| .com/en-us/azure/data-factory/int | structures within the data stores |
| roduction#datasets)               |                                   |
+-----------------------------------+-----------------------------------+
| [Linked                           | Linked services are much like     |
| Services](https://docs.microsoft. | connection strings to either data |
| com/en-us/azure/data-factory/intr | stores or compute resources       |
| oduction#linked-services)         |                                   |
+-----------------------------------+-----------------------------------+
| [Triggers](https://docs.microsoft | Triggers represent the unit of    |
| .com/en-us/azure/data-factory/int | processing that determines when a |
| roduction#triggers)               | pipeline execution needs to be    |
|                                   | kicked off.                       |
+-----------------------------------+-----------------------------------+
| [Control                          | Control flow is an orchestration  |
| Flow](https://docs.microsoft.com/ | of pipeline activities that       |
| en-us/azure/data-factory/introduc | includes chaining activities in a |
| tion#control-flow)                | sequence, branching, defining     |
|                                   | parameters at the pipeline level, |
|                                   | and passing arguments while       |
|                                   | invoking the pipeline on-demand   |
|                                   | or from a trigger.                |
+-----------------------------------+-----------------------------------+

 

 

Guidance
========

The following scenarios are well suited for Data Factory Pipeline:

 

+-----------------------------------+-----------------------------------+
| Scenario                          | Description                       |
+===================================+===================================+
| Azure data store load             | Separate control-flow to          |
|                                   | orchestrate complex patterns with |
|                                   | branching, looping, conditional   |
|                                   | processing                        |
+-----------------------------------+-----------------------------------+
| Lift-and-Shift to the Cloud       | Migrate on-premise data stores to |
|                                   | Azure                             |
|                                   |                                   |
|                                   | Lift-and-shift existing           |
|                                   | on-premise SSIS packages to cloud |
+-----------------------------------+-----------------------------------+
| Perform and incremental data load | Build Data-Driven, Intelligent    |
|                                   | SaaS Application                  |
|                                   |                                   |
|                                   | C\#, Python, PowerShell, ARM      |
|                                   | support                           |
+-----------------------------------+-----------------------------------+
|                                   | Customer profiling, Product       |
|                                   | recommendations, Sentiment        |
| Perform Big Data Analytics        | Analysis, Churn Analysis,         |
|                                   | Customized offers, customer usage |
|                                   | tracking, customized marketing    |
|                                   |                                   |
|                                   | On-demand Spark cluster support   |
+-----------------------------------+-----------------------------------+

 

-   Chain Logic Apps with Data Factory to create automated pipelines: use an Azure Logic App for data preparation by making data sets available in a specific data source and triggers Azure Data Factory for further processing. The Data Factory pipeline processes data in the data source and in turn triggers additional Azure Logic App(s) as required.

-   It is recommended that data encryption mechanism be enabled for [supported data stores](https://docs.microsoft.com/en-us/azure/data-factory/data-movement-security-considerations#data-encryption-at-rest).

-   When copying data between file-based stores, the default behavior (auto determined) usually give you the best throughput.

-   If the size of data you want to copy is large, you can adjust your business logic to further partition the data and schedule Copy Activity to run more frequently to reduce the data size for each Copy Activity run.

-   Establish a baseline. During the development phase, test your pipeline by using a representative data sample. If the performance you observe doesn\'t meet your expectations, you need to identify performance bottlenecks. When you\'re satisfied with the execution results and performance, you can expand the definition and pipeline to cover your entire data set.

-   Be cautious about the number of data sets and copy activities requiring Data Factory to connect to the same data store at the same time. Many concurrent copy jobs might throttle a data store and lead to degraded performance, copy job internal retries, and in some cases, execution failures.

-   [Performance and tuning guide](https://docs.microsoft.com/en-us/azure/data-factory/copy-activity-performance)

 

 

Preparation
===========

 

-   Get the [storage account name and account key](https://docs.microsoft.com/en-us/azure/data-factory/quickstart-create-data-factory-portal#azure-storage-account)

-   [Create the input folder and files](https://docs.microsoft.com/en-us/azure/data-factory/quickstart-create-data-factory-portal#create-the-input-folder-and-files)

-   [Secure the data store credentials ](https://docs.microsoft.com/en-us/azure/data-factory/data-movement-security-considerations#securing-data-store-credentials)

-   [Firewall configurations and whitelisting IP addresses](https://docs.microsoft.com/en-us/azure/data-factory/data-movement-security-considerations)

 

 

 

 

Procedure: Create a Data Pipeline
=================================

 

1.  Create a Data Factory by using the Azure Data Factory

    a.  [Azure Portal](https://docs.microsoft.com/en-us/azure/data-factory/quickstart-create-data-factory-portal#create-a-data-factory)

    b.  [PowerShell](https://docs.microsoft.com/en-us/azure/data-factory/quickstart-create-data-factory-powershell#create-a-data-factory)

 
-

1.  Monitor Data Factory

    a.  [Visually monitor Azure data factories ](https://docs.microsoft.com/en-us/azure/data-factory/monitor-visually)

    b.  [Monitor data factories using Azure Monitor](https://docs.microsoft.com/en-us/azure/data-factory/monitor-using-azure-monitor)

 

 

 
