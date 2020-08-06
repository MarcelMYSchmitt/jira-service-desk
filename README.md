# Introduction

This repository contains the on premise (via docker) set up of Jira Service Desk. In addition you can find the requests you need from the [official Atlassian documentation](https://developer.atlassian.com/cloud/jira/service-desk/rest/api-group-servicedesk/#api-group-servicedesk). 
  
You can use them for your on premise installation or in your hosted on cloud solution, just change the base path or every URL.   

<b>In general:</b>   
When you want to use Jira Service Desk you have to think about the projects you want to create/support there and how you want to support the customers inside your Service Desk. You can have just one project in one Jira Service Desk instance or multiple instances with different customers. It's like multi tenancy handling...maybe you do want to have some kind of seperation between projects and customers. Every customer can be part of an organization in Service Desk, organizations can be seen as a mirror of companies of your application.  

For creating and receiving requests automatically you have to think about accessing the APIs...do you want to have a personal or technical user? What are the permissions you have to set....?  

In the following you will hopefully get an answer of these questions.


---


## Accessing APIs

API Access will use basic authentication which means you will always use a non technical user for accessing all APIs.  
You can also use oAuth, described in the [REST API documentation](https://developer.atlassian.com/cloud/jira/service-desk/jira-rest-api-oauth-authentication/). In this repository you will always find the requests with basic authentication.


---


## Workflow

Functional and technical steps to achieve customer satisfaction concerning support functionality. 

We assume that we have following data: 
 - Name of the customer
 - E-Mail address of the customer
 - Company Name of the customer



### Possible workflow 


1. Check if organization exists

   ```
   If (exists) {
      take existing one
   } else {
      create new organzation
   }
   ```


2. Check if customer exists

   ```
   If (exists) {
      take existing one
   } else {
      create new customer
      add new customer to organzation
   }
   ```


3. Get internalServiceId from all Service Desks   

   We could have several service desks and maybe do want to create requests etc. in all, but just one of them. 
   So we are calling all existing service desks and look for a specific one with a special name to receive its `internal id`. 

   ```
   function ServiceDeskId (get all service desks) {
       retun internalServicedeskId you want
   }
   ```

In general 3. is optional -> we not need them if we already know the id nd make sure that they will not change in the future.  


4. Create request 


5. Get status and feedback from Support
   Customer has asked in step 1 for support and wants to see the current status of his request. 


6. Response from support did not help customer so he has to    
   comment/answer on the ticket.