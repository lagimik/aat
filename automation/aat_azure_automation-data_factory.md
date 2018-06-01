Overview
========

Azure Data Factory is a cloud-based data integration service to create data-driven workflows to orchestrating and automating data movement and data transformation. Data Factory uses data-driven workflows to orchestrate movement of data between supported data stores. Note that Azure Data Factory does not store any data except for linked service credentials for cloud data stores, which are encrypted by using certificates.

Azure Data Factory consists of the following concepts:




Concept	Description
Pipeline	A data factory might have one or more pipelines. A pipeline is a logical grouping of activities that performs a unit of work. Together, the activities in a pipeline perform a task. A Pipeline Run is an instance of the pipeline execution. Parameters are key-value pairs of read-only configuration. 
Activity	Activities represent a processing step in a pipeline. 
	Data Factory supports three types of activities: data movement activities, data transformation activities, and control activities.
Datasets	Datasets represent data structures within the data stores
Linked Services	Linked services are much like connection strings to either data stores or compute resources
Triggers	Triggers represent the unit of processing that determines when a pipeline execution needs to be kicked off. 
Control Flow	Control flow is an orchestration of pipeline activities that includes chaining activities in a sequence, branching, defining parameters at the pipeline level, and passing arguments while invoking the pipeline on-demand or from a trigger. 


Guidance
========
The following scenarios are well suited for Data Factory Pipeline:

Scenario	Description
Azure data store load	Separate control-flow to orchestrate complex patterns with branching, looping, conditional processing
Lift-and-Shift to the Cloud	Migrate on-premise data stores to Azure
	Lift-and-shift existing on-premise SSIS packages to cloud
Perform and incremental data load	Build Data-Driven, Intelligent SaaS Application
	C#, Python, PowerShell, ARM support
	Customer profiling, Product recommendations, Sentiment Analysis, Churn Analysis, Customized offers, customer usage tracking, customized marketing
Perform Big Data Analytics	On-demand Spark cluster support

	• Chain Logic Apps with Data Factory to create automated pipelines: use an Azure Logic App for data preparation by making data sets available in a specific data source and  triggers Azure Data Factory for further processing. The Data Factory pipeline processes data in the data source and in turn triggers additional Azure Logic App(s) as required.
	• It is recommended that data encryption mechanism be enabled for supported data stores. 
	• When copying data between file-based stores, the default behavior (auto determined) usually give you the best throughput. 
	• If the size of data you want to copy is large, you can adjust your business logic to further partition the data and schedule Copy Activity to run more frequently to reduce the data size for each Copy Activity run.
	• Establish a baseline. During the development phase, test your pipeline by using a representative data sample. If the performance you observe doesn't meet your expectations, you need to identify performance bottlenecks. When you're satisfied with the execution results and performance, you can expand the definition and pipeline to cover your entire data set.
	• Be cautious about the number of data sets and copy activities requiring Data Factory to connect to the same data store at the same time. Many concurrent copy jobs might throttle a data store and lead to degraded performance, copy job internal retries, and in some cases, execution failures.
	• Performance and tuning guide


Preparation
===========

	• Get the storage account name and account key
	• Create the input folder and files
	• Secure the data store credentials 
	• Firewall configurations and whitelisting IP addresses




Procedure: Create a Data Pipeline
=================================

	1. Create a Data Factory by using the Azure Data Factory
		a. Azure Portal
		b. PowerShell

	2. Monitor Data Factory
		a. Visually monitor Azure data factories 
		b. Monitor data factories using Azure Monitor


