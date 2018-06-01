2.3 Azure Database Workloads

Wednesday, March 7, 2018

12:39 PM

 

 

 

 

When to use
-----------

 

Use the procedure described in this section to implement disaster for PaaS database workloads. This scenario includes Azure SQL, Cosmos DB, and Data Lake.

 

Guidance
========

### Azure SQL

-   Leverage Azure SQL Database and Cosmos DB geo-replication to configure secondary database replicas in other regions. Secondary databases are available for querying and for failover in the case of a data center outage or the inability to connect to the primary database.

-   [Azure SQL Business Continuity](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-business-continuity) capabilities support standard geo-replication or active-geo-replication.

    -   **Standard geo-replication:** designed for applications that are using geo-replication to achieve disaster recovery SLA.

    -   **Active geo-replication:** designed for the applications with high-volume read-oriented workload could benefit from read-scale load balancing in addition to fast disaster recovery.

    -   To achieve RPO of \< 5 seconds and recovery times of less than 30 seconds active geo-replication is required.

###  

### Azure SQL Data Warehouse

-   By default, SQL Data Warehouse performs a geo-backup once per day to a paired data center. The RPO for a geo-restore is 24 hours. You can restore the geo-backup to a server in any other region where SQL Data Warehouse is supported. A geo-backup ensures SQL data warehouse can be restored in case the snapshots cannot be accessed in your primary region.

 

### Redis Cache

-   The disaster recovery posture of Redis Cache depends on its usage pattern. When used for web user session caching, geo-replication is generally not required. However, messaging and distributed transaction scenarios may require geo-replication to ensure recoverability requirements can be met.

 

### Cosmos DB

-   Cosmos DB failover handling is automatic without requiring code change of any kind.

-   SDK is auto-homing and will failover to next available region in the chosen list of regions.

-   There is no availability, performance loss during a manual failover. During DR-based failover potential unreplicated changes can be merged when the region returns to normal database situation.

-   see [How to distribute data globally with Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/distribute-data-globally) and [Automatic regional failover for business continuity in Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/regional-failover)

>  

 

 

Preparation
===========

 

Procedure
=========

1.  Azure SQL Geo-Replication and Failover Groups

    a.  [Failover groups and active geo-replication](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)

>  

1.  Azure Redis Cache Geo-Replication

    a.  [How to configure Geo-replication for Azure Redis Cache](https://docs.microsoft.com/en-us/azure/redis-cache/cache-how-to-geo-replication%3e)

>  

1.  Azure Cosmos DB Geo-Replication

    a.  [Add global database regions for Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/tutorial-global-distribution-sql-api%3e) and [How to distribute data globally with Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/distribute-data-globally)

<!-- -->

1.  Restore Azure SQL Data warehouse

    a.  [Restoring from restore points](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/backup-and-restore) and [Geo-redundant restore](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/backup-and-restore)

>  
>
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

 