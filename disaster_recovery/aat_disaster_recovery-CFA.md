1.3 Component Failure Analysis

Friday, December 15, 2017

8:41 AM

 

Guidance
========

 

 

 

Preparation
===========

 

Leverage the [Technical Dependency Analysis](onenote:#1.2%20Technical%20Dependency%20Analysis&section-id={F0BE61F6-6020-49D3-8FB9-B0323B63A0B7}&page-id={1F53308D-0D65-4D59-9357-760A8C5A785A}&end&base-path=https://microsoft.sharepoint.com/teams/AATDevelopment2/SiteAssets/AAT%20Development%20Notebook/Disaster%20Recovery%20(Work%20in%20Progess).one) to identify the services for each business process.

 

Procedure
=========

 

1.  Conduct a Component Failure Analysis

> Using a spreadsheet, create a grid with business processes on one axis and the dependent Azure services on the other.
>
>  

  **Business Process / Function**   **Service 1**   **Service 2**   **Service 3**   **...**   **Service n**
  --------------------------------- --------------- --------------- --------------- --------- ---------------
  Process 1                                                                                    
  Process 2                                                                                    
  Process 3                                                                                    
  ...                                                                                          
  Process n                                                                                    

>  

a.  Leave a blank when a failure of the Azure service does not impact the business process in any ways;

b.  Insert an 'X' when the failure of the Azure service causes the business process to be inoperative;

c.  Insert an 'A' when there is an alternative to provide the service; and

d.  Insert an 'M' when there is an alternative service, but the service requires manual intervention to be recovered.

<!-- -->

1.  Conduct and Impact Assessment

    a.  Identify Single Points of Failure (SPoF)

    b.  Identify the Business/Customer impact of this service failing in terms of users and / or business cost.

    c.  Identify the probability of failure and mitigation approaches to avoid this impact.

        i.  Design changes to prevent this impact 

        ii. Redundancy or some form of resiliency 

        iii. Additional cost considerations

 
