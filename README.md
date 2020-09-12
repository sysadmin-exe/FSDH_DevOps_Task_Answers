# FSDH_DevOps_Task_Answers
This is a Repo that contains the answers to the DevOps task from FSDH

## Diagram showing architecture

![Alt Text](https://terraformlearn0702.blob.core.windows.net/files/serverless_architecture.png) 

This Diagram contains 2 regions for HA accessible via traffic manager. Azure Function App has been used for the API (middle tier) to give us the Serverless set up. Cient/Mobile app will be on Azure web app. These app resources will be deployed in an app service plan. Azure SQL and Cosmos NoSQL will be used as they have cross regional replication features and is highly available so one set up is enough to meet the needs of the 2 regions. 

## CI/CD Strategy
The CI/CD Pipeline will be created and managed with **Azure DevOps.** 
- Developers will push code and subsequent code changes from they PCs where they have tested code locally to the Azure DevOps Repo for the Organization.
- A pipeline will be created for 3 Deployments - Dev, QA and Prod.
- Each deployment starting from Dev will have to go through all necessary check and approval has to be given for the next deployment to proceed on the pipeline till production is reached. 
- Build will be automatic so that once code changes are commited, the pipeline does the needed deployment work.

![Alt Text](https://terraformlearn0702.blob.core.windows.net/files/Azure_DevOps_Pipeline.png)

## IaC Tool of choice
**Terraform.** With the use of modules, we can deploy same enviroment in different regions easily.

## Go-Live Plan
- Get all stakeholders on board. From developers, to testers, to project managers and product team. This can be a meeting in a triage from. We then create a Go live plan together as I dont think one person or one group can create a go live plan. 
- Have some user testing like Beta testing where we have selected users (not developers) check out the app to let us know what they think and if they had any issues.
- Security tests to make sure the application can withstand web application attacks.
- Test dependencies - Unit testing. This will help us know how each tier or resource in this application combines together to give a product. Test to know what kind of issues can occur should one part of the application go down and how long it can take to recover. 
- Ensure that prior to go live, the application is using the updated version of any resource. Since this application uses mostly PaaS resources, we might not have to bother but this should still be noted.
- Check for SSL certificate status and expiration date.
- Make sure domain name is still intact. We dont want to be having issues with domain few days after go live.
- Do a test go live. This can be simulated or the real deal but without letting anyone outside the development team knowing like press.
- Have a go live time period and stick to it. This should not be on fridays or holidays so that we dont have a absent team member in case issues occur.
- Have a rollback plan if this an already exixting software.
- Monitor! Monitor!! Monitor!!! Then wait for feedback. 

## Monitoring
Azure Log Analytics & Application Insights: This will be used to check metrics like Requests per second on API and web app, Capacity, Failed requests, Performance, health status of resources. 
Alerts will also be set up to trigger emails to development team in the case of unexpected behaviour.
