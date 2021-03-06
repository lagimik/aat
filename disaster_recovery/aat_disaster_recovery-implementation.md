
Azure Disaster Recovery Implementation
======================================

Traditionally, organizations have taken a 'one size fits all' approach and essentially created common DR processes regardless of business priorities, objectives, and business impacts. For example by systematically replicating complete production environments from one datacenter to another, often with considerable hardware and software investments. Invariably this ends up being both expensive and an ineffective use of company resources.

With composite solutions consisting of Software as a Service (SaaS), Platform as a Service (PaaS), and Infrastructure as Service (IaaS) components it is important to clearly delineate between responsibilities of the cloud provider and the consumer. The following summarizes these responsibilities with respects to the Microsoft cloud services:

 

  **Service Type**   **Disaster Recovery Responsabilities**
  ------------------ -------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **SaaS**           Microsoft will maintain the solution according the state SLA. Services will failover to Azure secondary regions without customer involvement.
  **PaaS**           Microsoft and Customer may responsibility for service continuity depending on the service. Services will need to be reviewed on a case-by-case basis.
  **IaaS**           Customer is responsible for service continuity. IaaS-based will not failover to secondary Azure region unless additional measures are configured by the customer.

If a region-wide service disruption occurs, the locally redundant copies of your data are not available. If you have enabled geo-replication, there are three additional copies of your blobs and tables in a different region. If Microsoft declares the region lost, Azure remaps all of the DNS entries to the geo-replicated region.


Guidance
========

* Leverage the business continuity capabilities of the SaaS service provided by the cloud provider. Focus business continuity efforts on PaaS and IaaS components of the solution.

* Services such as DNS, Active Directory have built-in mechanisms for replicating the state that should be used when feasible.

* Leverage Azure Traffic Manager if services are already deployed and dormant in the secondary region

* Weigh business and compliance requirements, cost, and complexity as inputs to DR strategy by business function. The following table summarizes the high-level patterns for the *PaaS and IaaS* services in addition to their implications in terms of RTO, Complexity, and Cost.


| **DR Pattern**| **Descriptiopn**  | **RTO**     | **Complexity** | **Cost**    |
|---------------|-------------------|-------------|----------------|-------------|
|[Azure Site Recovery](https://docs.microsoft.com/en-us/azure/architecture/resiliency/disaster-recovery-azure-applications#failover-using-azure-site-recovery)|Azure Site Recovery, it creates several resources in the secondary region: Resource group, Virtual network (VNet), Storage account, Availability sets to hold VMs after failover.|
|[Redeploy to Secondary Region](https://docs.microsoft.com/en-us/azure/architecture/resiliency/disaster-recovery-azure-applications#database-only)|only the primary region has applications and databases running. The secondary region is not set up for an automatic failover. So when a disaster occurs, you must spin up all the parts of the service in the new region. This includes uploading a cloud service to Azure, deploying the cloud service, restoring the data, and changing DNS to reroute the traffic.|
|[Active / Passive (Database Only)](https://docs.microsoft.com/en-us/azure/architecture/resiliency/disaster-recovery-azure-applications#database-only)|All traffic goes to the active site. The data is active on both regions with synchronization mechanisms in place.If a disaster occurs, the virtual machines, services and applications are restored on the DR site. Traffic is routed to the DR site.|
|[Active / Passive (Full Replica)](https://docs.microsoft.com/en-us/azure/architecture/resiliency/disaster-recovery-azure-applications#full-replica) | All traffic goes to the active site. The data, virtual machines, services and applications are active on both regions with synchronization mechanisms in place. If a disaster occurs, the DR environment is scaled-out as necessary. Traffic is routed to the DR site. |
|[Active / Active](https://docs.microsoft.com/en-us/azure/architecture/resiliency/disaster-recovery-azure-applications#active-active) |The data, virtual machines, services and applications are deployed and active on both primary production and secondary production site. Traffic is load balanced between the sites. If a disaster occurs at either site, the traffic is routed exclusively to the active site. The active site is scaled-out as necessary.|




Next Steps
----------

### 1. Implement [Secondary Region Prerequisites]()

### 2. Define DR strategy for [Azure Database Workloads](e) such as Azure SQL, Cosmos DB, Redis Cache

### 3. Define DR strategy for [Azure Stateful Workloads]() such as Virtual Machines and VDI such as Citrix.

### 4. Define DR strategy for [Azure Stateless Workloads]()

### 5. Define DR strategy for [Azure Storage]()

### 6. Define DR strategy for [D365]()

### 7. Conduct [Azure Disaster Recovery Simulation and Gap Analysis]() to identify gaps between the business process recovery requirements (RPO, RTO) and the recovery capabilities of the applications and supporting infrastructure (RPE, RTE)