.4 Azure Stateful Workloads

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



 

 