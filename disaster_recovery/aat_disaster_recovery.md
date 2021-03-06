


2.4 Azure Stateful Workloads

Friday, December 15, 2017

1:47 PM

 

 

Use the procedure described in this section to enable Azure Site Recovery for stateful workloads.

 

 

When to Use
-----------

 

This pattern is useful when you want to failover and recover stateful virtual machines from the primary Azure data centre to the secondary Azure data centre in the same region.

 

Replication is handled by replicating the disk configuration to a secondary set of storage accounts via the Site Recovery Agent Service that is automatically installed once the service has been configured.

In case of an outage, failover of specific workloads to the secondary region can be triggered. Failback to the primary site is also possible when running from the secondary site.

RPOs are usually 30 seconds or less.

  **Advantages**                                                                                                                                                                                                          **Disadvantages**
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  The configuration, failover and recovery are all managed from the Azure portal                                                                                                                                          Windows & Linux Red Hat virtual machines are supported, for the exhaustive list consult this [document: ](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-support-matrix-azure-to-azure)
  This method can work with any workload supported in Azure VMs. Application specific testing in this [workload summary.](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-workload#workload-summary)   Replicating Virtual Machines is only supported within the same subscription,
  App-agnostic, app-consistent, near-synchronous replication.                                                                                                                                                              
  Can integrate with SQL Always On to handle snapshots and app consistency                                                                                                                                                 
  Disaster drills can take place without impacting production or replication                                                                                                                                               
  Integration with Azure Automation capabilities                                                                                                                                                                           
  Seamless connection with currently planned Azure services, including network management, load balancers and Traffic Manager                                                                                              

 

Guidance 
=========

 

-   Azure Site Recovery RPO will be dependent on the amount of churn in the environment and the network bandwidth.  For example, if a system that is changing frequently (IOPS on the disk), replication of the changes to that environment will be rather high.  If the connectivity from that environment is so poor that the bandwidth can't transmit all of those changes, the RPO probably will not be achieved. 

 

-   With Azure Backup, the RPO is dependent on the frequency of your backups, but the RTO will again be dependent on bandwidth and capacity (i.e. a single file restore is much faster than an entire system).

 

 
=

Preparation
===========

 

1.  Capacity Planning

    a.  Use the [Capacity Planner for Azure Site Recovery DR Solution](https://gallery.technet.microsoft.com/Azure-Recovery-Capacity-d01dc40e) to to analyze the source environment (workloads) on Hyper-V or VMware or Physical server, bandwidth requirements, resource requirements (VMs, storage) on the target and any additional server resources that are required on the source side (SC VMMs, Configuration Servers, Process Servers etc).

    b.  Use the [Site Recovery Deployment Planner for Hyper-V to Azure](https://docs.microsoft.com/en-us/azure/site-recovery/hyper-v-deployment-planner-overview) to profile the environment and allocate sufficient bandwidth based on your daily data-change rate to meet your desired Recovery Point Objective (RPO)

 
=

Procedure
=========

 

1.  Azure Site Recovery for Stateful Web Tier:

    a.  [Replicate a multi-tier IIS-based web application](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-iis)

<!-- -->

1.  Azure Site Recovery for SQL Server Instance

    a.  [Protect SQL Server using SQL Server disaster recovery and Azure Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-sql)

<!-- -->

1.  Azure Site Recovery for Citrix

    a.  [Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-citrix-xenapp-and-xendesktop%3e)

>  

\* *

>  

 

 

MICROSOFT MAKES NO WARRANTIES, EXPRESS OR IMPLIED, IN THIS DOCUMENT.  

Complying with all applicable copyright laws is the responsibility of the user.  Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.  

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.  Except as expressly provided in any written license agreement from Microsoft, our provision of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.  

The descriptions of other companies' products in this document, if any, are provided only as a convenience to you.  Any such references should not be considered an endorsement or support by Microsoft.  Microsoft cannot guarantee their accuracy, and the products may change over time. Also, the descriptions are intended as brief highlights to aid understanding, rather than as thorough coverage. For authoritative descriptions of these products, please consult their respective manufacturers. 

© 2017 Microsoft Corporation. All rights reserved. Any use or distribution of these materials without express authorization of Microsoft Corp. is strictly prohibited. 

Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries. 

The names of actual companies and products mentioned herein may be the trademarks of their respective owners. 

 

 

2.5 Azure Stateless Workloads

Wednesday, March 7, 2018

12:39 PM

 

> Use the procedure described in this section to implement disaster for stateless workloads.
>
>  

When to use
-----------

>  
>
> This scenario could apply to the following: stateless app servers running on Virtual Machines, Platform Services such as Logic Apps and Functions that use storage accounts as back-end storage
>
>  

-   Re-deploy stateless resources through automation.

-   Access to their data sets can be insured by replicating the data layer using Geo-Redundant Storage or other Platform services.

>  
>
>  

+-----------------------------------+-----------------------------------+
| **Advantages**                    | **Disadvantages**                 |
+===================================+===================================+
| Read-access geo-redundant storage | Applications manage which         |
| (RA-GRS) maximizes availability   | endpoint it is interacting with   |
| for your storage account. RA-GRS  | when using RA-GRS. ( The          |
| provides read-only access to the  | secondary endpoint is similar to  |
| data in the secondary location,   | the primary endpoint, but appends |
| in addition to geo-replication    | the suffix --secondary to the     |
| across two regions.               | account name)                     |
|                                   |                                   |
|                                   | \* *                              |
|                                   |                                   |
|                                   |                                   |
+-----------------------------------+-----------------------------------+
| Azure Storage typically has an    | The proposed solution assumes     |
| RPO of less than 15 minutes,      | that it is acceptable to return   |
|                                   | potentially stale data to the     |
|                                   | calling application. Because data |
|                                   | in the secondary region is        |
|                                   | eventually consistent, it is      |
|                                   | possible the primary region may   |
|                                   | become inaccessible before an     |
|                                   | update to the secondary region    |
|                                   | has finished replicating.         |
+-----------------------------------+-----------------------------------+

>  
>
>  

Guidance
========

>  
>
>  

-   Consider Re-Deployment over replication when feasible for stateless layers.

    -   Stateless servers should be redeployed using Infrastructure as Code (ARM templates) when feasible. Leverage template parameters to minimize the changes required to the templates.

    -   Asynchronously replicate the data stores (such as SQL Azure database, Blob Storage, or CosmosDB) using the respective features of these services such as using Geo-Redundant Storage or other Platform services

>  

-   If RTO does not allow time for redeployment, the recommendation is to deploy all primary region resources in a secondary region also. Primary region resources include:

    -   *Azure Service Bus*

    -   *Azure Event Hubs *

    -   *Azure API Management*

    -   *Azure Logic Apps*

###  

### Service Bus

-   The disaster recovery feature implements metadata disaster recovery, and relies on primary and secondary disaster recovery namespaces. Note that the Geo-disaster recovery feature is available for the [Premium SKU](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-premium-messaging) only.

-   By pairing azure service bus namespaces in different regions an *alias* can be created. The alias provides a single stable Fully Qualified Domain Name (FQDN) connection string. Applications use this alias connection string to connect to a namespace.

-   Consider creating a durable client-side queue as a backup.

###  

### Event Hubs

-   Event Hub, much like Service Bus, requires the pairing of namespaces across regions as described in [Azure Event Hubs Geo-disaster recovery](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-geo-dr). The Geo-disaster recovery feature is globally available for the Event Hubs Standard SKU.

-   By pairing Azure Event Hub namespaces in different regions an *alias* can be created. The alias provides a single stable Fully Qualified Domain Name (FQDN) connection string. Applications use this alias connection string to connect to a namespace.

>  

### API Management

-   The service \"backup and restore\" feature provides the necessary building block for implementing your disaster recovery strategy. Backup is a long running operation that may take multiple minutes to complete.

-   Restore is a long running operation that may take up to 30 or more minutes to complete.

###  

### Function Apps

-   With Azure Durable Functions all state is persisted in Azure Storage.

>  

### Logic Apps

-   Deploy Logic Apps can be deployed through ARM templates in multiple regions to achieve redundancy in either active, or passive (disabled) mode.

-   Note that Logic Apps endpoints are not supported by Traffic Manager, therefore traffic cannot be redirected dynamically. Options includes:

    -   Making the calling or subscribing application aware of the primary and secondary endpoints so they can call the correct endpoint in the event of a failover.

    -   Use API Management to provide an endpoint traffic manager can reach and have API Management can then relay requests to Logic Apps.

<!-- -->

-   For B2B scenarios involving X12, AS2, and EDIFACT, see [Logic Apps B2B cross-region disaster recovery](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-b2b-business-continuity)

> \* *
>
>  

### Data Factory

-   Manage all the data factory code through a Visual Studio project.

>  
>
>  

Preparation
===========

>  

-   Harden your application by using [Best practices for insulating applications against Service Bus outages and disasters](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-outages-disasters/).

>  

Procedure
=========

>  

-   Azure Service Bus

    -   [Azure Service Bus Setup and Failover Flow](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-geo-dr#setup-and-failover-flow)

    -   Initiate pairing through Azure Portal Azure Service Bus blade or pair Azure Service Bus namespaces and create a namespace alias with the followin: [Enable Service Bus Geo-DR configurations using PowerShell](https://blogs.msdn.microsoft.com/servicebus/2018/02/16/enable-service-bus-geo-dr-configurations-using-powershell/)

>  

-   Azure API Management

    -   Use API Management as the endpoint for Traffic Manager with PowerShell [Add-AzureTrafficManagerEndpoint](https://docs.microsoft.com/en-us/powershell/module/azure/add-azuretrafficmanagerendpoint?view=azuresmps-4.0.0)

    -   Backup API Management with PowerShell [Backup-AzureRmApiManagement ](https://msdn.microsoft.com/en-us/library/mt619281.aspx)

    -   Restore API Management in secondary region with PowerShell[Restore-AzureRmApiManagement](https://msdn.microsoft.com/en-us/library/mt619278.aspx)

>  

-   Azure Functions

    -   This pattern consists of deploying a backup (passive) function app to a different region. Traffic Manager will monitor the primary (active) function app for availability. It will fail over to the backup function app if the primary fails.

    -   For durable functions, use Read-access geo-redundant storage (-RAGRS), which replicates your data to a secondary region and provides read-only access to the data in the secondary location.

>  

-   Azure Logic Apps

    -   Import Logic App into API Management with [Import a Logic App as an API](https://docs.microsoft.com/en-us/azure/api-management/import-logic-app-as-api)

>  
>
>  

-   Azure Data Factory

    -   Set up a development data factory with VSTS and [continuous integration lifecycle](https://docs.microsoft.com/en-us/azure/data-factory/continuous-integration-deployment#continuous-integration-lifecycle) to author Data Factory resources such as pipelines, datasets, and so forth. Redeploy to secondary regions in the event of a primary data center failure.

>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
> MICROSOFT MAKES NO WARRANTIES, EXPRESS OR IMPLIED, IN THIS DOCUMENT.  
>
> Complying with all applicable copyright laws is the responsibility of the user.  Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.  
>
> Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.  Except as expressly provided in any written license agreement from Microsoft, our provision of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.  
>
> The descriptions of other companies' products in this document, if any, are provided only as a convenience to you.  Any such references should not be considered an endorsement or support by Microsoft.  Microsoft cannot guarantee their accuracy, and the products may change over time. Also, the descriptions are intended as brief highlights to aid understanding, rather than as thorough coverage. For authoritative descriptions of these products, please consult their respective manufacturers. 
>
> © 2017 Microsoft Corporation. All rights reserved. Any use or distribution of these materials without express authorization of Microsoft Corp. is strictly prohibited. 
>
> Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries. 
>
> The names of actual companies and products mentioned herein may be the trademarks of their respective owners. 

 

2.6 Azure Storage

Wednesday, March 7, 2018

12:39 PM

 

 
=

 

Microsoft Azure Storage is the Microsoft-managed cloud service that provides storage in the Azure cloud. It consists of three data services: Blob Storage, File Storage and Queue Storage.

Azure Storage can be used as a discreet service, or it can underpin other Azure services that you are consuming. Data is stored in storage accounts.

At the region level, this is referred to as Locally-Redundant storage (LRS) which means that multiple copies of your data are maintained in a given region.

When to Use
===========

 

For Disaster Recovery in case of a region outage, Geo-Redundant Storage is designed to provide 16 9s durability by maintaining the local copies of your data in the primary region plus another set of copies of your data in the secondary region (ex: Canada Central is replicated to Canada East)

When a regional disaster affects a primary region, Microsoft will try to restore the service in that region. Dependent upon the nature of the disaster and its impacts, in some rare occasions we may not be able to restore the primary region. At that point, we will perform a geo-failover.

 

  **Advantages**                                                                                                                                                                                                                                                                                                               **Disadvantages**
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  At all times, Azure will keep and manage multiple copies of your data.                                                                                                                                                                                                                                                       Before and during the geo-failover, you won\'t have write access to your storage account due to the impact of the disaster but you can still read from the secondary if your storage account has been configured as RA-GRS
  Storage geo-failover will only be triggered by the Azure Storage team -- there is no customer action required.                                                                                                                                                                                                                
  existing storage service endpoints for blobs, tables, queues, and files will remain the same after the failover; the Microsoft-supplied DNS entry will need to be updated to switch from the primary region to the secondary region. Microsoft will perform this update automatically as part of the geo-failover process.    
  Before and during the geo-failover, you won\'t have write access to your storage account due to the impact of the disaster but you can still read from the secondary if your storage account has been configured as RA-GRS                                                                                                    

 

Guidance
========

 

### Azure Blob Storage

-   When the geo-failover has been completed and the DNS changes propagated, read and write access storage accounts will be resumed if GRS or RA-GRS configured for the storage account.

-   Query [\"Last Geo Failover Time\" of your storage account](https://msdn.microsoft.com/library/azure/ee460802.aspx) to get more details noting the value of the following fields: StatusOfPrimary, LastGeoFailoverTime

-   After the failover, a storage account will be fully functioning, but in a \"degraded\" status, as it is actually hosted in a standalone region with no geo-replication possible. To mitigate this risk, Microsoft will restore the original primary region and then do a geo-failback to restore the original state. If the original primary region is unrecoverable, we will allocate another secondary region.

-   For more details on the infrastructure of Azure Storage geo replication, please refer to the article on the Storage team blog about [Redundancy Options and RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

### Azure Data Lake

-   Critical Data is Azure Data Lakes should be copied to another Data Lake Store account in another region with a frequency aligned to the needs of the disaster recovery plan.

-   Understand the different capabilities between storage offerings: [Comparing Azure Data Lake Store and Azure Blob Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-comparison-with-blob-storage)

>  

Procedure
=========

 
-

1.  Azure Blob Storage

    a.  Enable Read-access geo-redundant storage (RA-GRS) Replication on storage account. See replication options under [create a general purpose storage account](https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-account?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&tabs=portal#create-a-general-purpose-storage-account)

<!-- -->

1.  Azure Data Lake

    a.  L. Azure Data Factory is a useful service for creating and deploying data moveeverage [ADLCopy](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob), [Azure PowerShell](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell) or [Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-store)ment pipelines on a recurring basis.

>  

 

 

MICROSOFT MAKES NO WARRANTIES, EXPRESS OR IMPLIED, IN THIS DOCUMENT.  

Complying with all applicable copyright laws is the responsibility of the user.  Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.  

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.  Except as expressly provided in any written license agreement from Microsoft, our provision of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.  

The descriptions of other companies' products in this document, if any, are provided only as a convenience to you.  Any such references should not be considered an endorsement or support by Microsoft.  Microsoft cannot guarantee their accuracy, and the products may change over time. Also, the descriptions are intended as brief highlights to aid understanding, rather than as thorough coverage. For authoritative descriptions of these products, please consult their respective manufacturers. 

© 2017 Microsoft Corporation. All rights reserved. Any use or distribution of these materials without express authorization of Microsoft Corp. is strictly prohibited. 

Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries. 

The names of actual companies and products mentioned herein may be the trademarks of their respective owners. 

 

2.7 D365

Friday, May 25, 2018

8:46 AM

 

The Dynamics 365 for Finance and Operations production environments are configured with disaster recovery support that includes disaster recovery capabilities of stateful and stateless workloads:

 

-   Azure SQL active-geo replication for primary databases, with a Recovery Point Estimate (RPO) of \< 5 seconds.

-   Geo-redundant copies of Azure blob storage (containing document attachments) in other Azure regions.

-   Same secondary region for the Azure SQL and Azure blob storage replications.

 

Stateful D365 Components
------------------------

The primary data stores are supported for replication. This means that Dynamics 365 for Finance and Operations application components, such Management Reporter and Entity store, use transformed data from the primary database, which need to be generated after the recovery site has been set up and the service has started.

 

Stateless D365 Components
-------------------------

Customer code artifacts and recovered data stores is used to re-deploy the site, with a Recovery Time Objective (RTO) of up to 10 hours. This will enable state replication of the compute nodes along with networking and other components to set up the secondary site using the recovered data stores. Refer to Table 6 for more information about the roles and responsibilities for disaster recovery

 

 

API Integration 
----------------

Applications that do not link to the Microsoft Dynamics 365 SDK assemblies, for example Java applications that access the web services by using SOAP or ODATA, can try accessing the failover URL for the target organization.

 

The URL for a failover alternate organization is the same as the URL for the primary organization with "\--s" added to the organization name. For example, an organization named Contoso would have the primary and alternate URLs shown in the following table.

 

  **Primary Organization URL**             **Alternate Organization URL**
  ---------------------------------------- -------------------------------------------
  <https://contoso.api.crm.dynamics.com>   <https://contoso--s.api.crm.dynamics.com>

For non.NET-connected applications, there is no notification event to which your application can subscribe to receive notice of a service interruption and failover. Your application will begin to receive a variety of fault exceptions, as listed previously, during the service interruption. At that point, the application can attempt to connect to the failover alternate URL for the target organization. After the disaster has been corrected, a fail back to the primary URL for the organization occurs as part of planned organization maintenance.

 

 

3.0 Azure Disaster Recovery Simulation and Gap Analysis

Friday, December 15, 2017

8:41 AM

 

 

Use this guide to plan and execute disaster recovery simulations to confirm recovery point and recovery time estimate, identify gaps, and mitigation plans.

 

Guidance
========

-    

-   The intent of this testing is to evaluate the feasibility of the recovery plan and highlight any issues that were inadequately addressed.

-   Execute simulations so that the created scenarios don\'t disrupt actual business, while still simulating real situations.

-   The simulated scenarios must be completely controllable such that services can be restored even if the tested recovery plan fails.

-   Ensure any regulatory reporting requirements related to DR are considerer

-   Refer to [disaster simulation](https://docs.microsoft.com/en-us/azure/architecture/resiliency/disaster-recovery-azure-applications#disaster-simulation) in *Disaster recovery for Azure applications*.

 

Preparation
===========

 
-

-   Determine the tolerance for production downtime during DR testing affects the design. There are three basic scenarios:

    -   Zero tolerance for production downtime -- the DR test must be executed without bringing down production.

    -   Regular Maintenance Window -- the DR test must be executed during a regular maintenance window.

    -   Extended Maintenance Window -- special allowance is made for an extended outage during the DR test

-   Define the level of integration testing that will be required during the DR test. This covers integration into existing 3rd systems and 3rd party systems

-   Define data consistency requirements on how data consistency (between DR and Prod) is confirmed.

-   Define the scope of DR testing process: full regression testing of the entire system, functional testing, or smoke testing.

 

<table>
<thead>
<tr class="header">
<th><strong>Cloud Service</strong></th>
<th><strong>Used In</strong></th>
<th><p><strong>RTO </strong></p>
<p> </p></th>
<th><p><strong>RPO </strong></p>
<p> </p></th>
<th><p><strong>RTE </strong></p>
<p> </p></th>
<th><p><strong>RPE </strong></p>
<p> </p></th>
<th><strong>Workload Type</strong></th>
<th><strong>DR Approach</strong></th>
<th><strong>Test</strong></th>
<th><strong>Gap</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Microsoft Cloud Service 1</strong></td>
<td>&lt;dependencies&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;SaaS, PaaS, IaaS&gt;</td>
<td><p>&lt;Database, Stateful,</p>
<p>Stateless, Storage&gt;</p></td>
<td> </td>
<td> </td>
</tr>
<tr class="even">
<td><strong>Microsoft Cloud Service 2</strong></td>
<td>&lt;dependencies&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;SaaS, PaaS, IaaS&gt;</td>
<td><p>&lt;Database, Stateful,</p>
<p>Stateless, Storage&gt;</p></td>
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td><strong>Microsoft Cloud Service 3</strong></td>
<td>&lt;dependencies&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;SaaS, PaaS, IaaS&gt;</td>
<td><p>&lt;Database, Stateful,</p>
<p>Stateless, Storage&gt;</p></td>
<td> </td>
<td> </td>
</tr>
<tr class="even">
<td><strong>…</strong></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td><strong>Microsoft Cloud Service n</strong></td>
<td>&lt;dependencies&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;hours&gt;</td>
<td>&lt;minutes&gt;</td>
<td>&lt;SaaS, PaaS, IaaS&gt;</td>
<td><p>&lt;Database, Stateful,</p>
<p>Stateless, Storage&gt;</p></td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>

 

 

Procedure
=========

 

1.  Azure Stateful Workload Disaster Recovery Simulation

    a.  [Run a disaster recovery drill for Azure VMs to a secondary Azure region](https://docs.microsoft.com/en-us/azure/site-recovery/azure-to-azure-tutorial-dr-drill)

>  

1.  Azure Database Workload Disaster Recovery Simulation

    a.  [Fail over to a geo-replicated secondary server using the Azure portal ](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-portal)

    b.  [Fail over to the secondary server using PowerShell](https://docs.microsoft.com/en-us/azure/sql-database/scripts/sql-database-setup-geodr-and-failover-database-powershell)

>  

1.  Azure Stateless Workload Disaster Recovery Simulation

>  

1.  Azure Storage Disaster Recovery Simulation

    a.  [Simulate a failure in accessing read-access redundant storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-simulate-failure-ragrs-account-app?tabs=windows)

\* *

 

 

MICROSOFT MAKES NO WARRANTIES, EXPRESS OR IMPLIED, IN THIS DOCUMENT.  

Complying with all applicable copyright laws is the responsibility of the user.  Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.  

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.  Except as expressly provided in any written license agreement from Microsoft, our provision of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.  

The descriptions of other companies' products in this document, if any, are provided only as a convenience to you.  Any such references should not be considered an endorsement or support by Microsoft.  Microsoft cannot guarantee their accuracy, and the products may change over time. Also, the descriptions are intended as brief highlights to aid understanding, rather than as thorough coverage. For authoritative descriptions of these products, please consult their respective manufacturers. 

© 2017 Microsoft Corporation. All rights reserved. Any use or distribution of these materials without express authorization of Microsoft Corp. is strictly prohibited. 

Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries. 

The names of actual companies and products mentioned herein may be the trademarks of their respective owners. 

 
