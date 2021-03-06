# Azure Secondary Region Prerequisites

## When to use

Use the procedure described in this section to prepare Azure secondary site for disaster recovery of PaaS and IaaS services

## Guidance

* The simplest approach, requiring no action, is to wait until the region is restored. This is recommended for short term outages and for workloads with less stringent availability requirements. The current service status on the [Azure Service Health Dashboard](https://azure.microsoft.com/status/)

* For workloads with more demanding continuity requirements, preparing the secondary data center is necessary. A number of ancillary services and configurations are expected to be pre-defined, configured and running in Lowes's subscription in the secondary region to facilitate failover activities and testing.

* Azure Traffic Manager automates the failover of user traffic to another region if the primary region fails. Traffic Manager detects a failure in the primary site and rolls over to the failover site, regardless of whether that site is currently serving users.

* The following services should be predefined and configured ahead of time: Azure Virtual Networks, Azure RBAC Assignment, Active Directory Domain Services, Domain Name Services, JumpBox VMs, Systems Center Configuration Manager, Certificate Services (PKI)

## Procedure

### 1.  Azure RBAC Assignment
* Security & Access of Azure subscriptions to be maintained with same governance as primary datacenter.

### 2.  Azure Virtual Networks
* Continuously deploy and maintain Virtual Networks, Subnets, S2S VPN and any other network components. Note: Two VNets using the same private IP address space and resources in two different regions ahead of time.

### 3. Active Directory and Internal Domain Name Services
* An availability set of virtual machines (2) to be replicated from the primary region and/or the on-premises domain controllers. Running on AD Domain Controllers, AD-integrated DNS will provide internal name resolution. See [Use Azure Site Recovery to protect Active Directory and DNS](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-active-directory)

### 4. Jumpbox VMs
* For workstations that will be used for system administration see Citrix information under [Azure Stateful Workloads](onenote:#2.3%20Azure%20Stateful%20Workloads&section-id={F0BE61F6-6020-49D3-8FB9-B0323B63A0B7}&page-id={B64468F6-B3B9-4D87-AEBE-C86174EB2BD4}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Disaster%20Recovery%20(Work%20in%20Progess).one)

### 5. System Center Configuration Manager
* [Configuration Manager on Azure](https://docs.microsoft.com/en-us/sccm/core/understand/configuration-manager-on-azure)
* If Configuration Manager cloud-based distribution points are to be used, Public key infrastructure (PKI) certificates must be installed on the site server for authentication.
* Any task sequences deployed to Azure virtual machines configured to use SCCM must be configured as **Download all content locally**.
* PXE and multicast, streamed applications, Apple and Unix clients, Windows and third-party updates are not supported features of cloud-based distribution points

### 6.  Integration Account
* Identify a secondary region and create an [integration account](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-create-integration-account) in the secondary region.

### 7. Azure Traffic Manager
* Azure Traffic Manager provides multiple [routing methods](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-routing-methods), so you can choose whether to manage your deployments using a primary/backup model or to split traffic between them. Service failover to a set of identical backup services can be done through [configuring the priority traffic routing method](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-configure-priority-routing-method)