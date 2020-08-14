# Introduction

This repository contains the on premise (via docker) set up of Jira Service Desk. In addition you can find the requests you need from the [official Atlassian documentation](https://developer.atlassian.com/cloud/jira/service-desk/rest/api-group-servicedesk/#api-group-servicedesk). 
  
You can use them for your on premise installation or in your hosted on cloud solution, just change the base path or every URL.   


<b>In general:</b>   

In general you have to think about how the customer will interact with this Service Desk. Do you want him to interact directly with the Service Desk or do you want to provide him a custom user interface within your application? If you want to provide him an own interface you can find all relevant API calls below. Advantage of providing an own user interface could be a better UI/UX flow within your application and besides, concerning Jira Service Desk, also a cost issue. If you would use Jira Service Desk directly you would have to add every customer separately. In your own onpremise installation it could be no problem, but if you use something on cloud you could pay per user. The provided solution here, "fakes" adding customers to the Service Desk. They will be added but will not use the Desk. You will always use the API with a technical user. And the user will not realize this...just make sure that you disable all email notifications in your settings. So the user will not now that there is a Jira Service Desk running in the background.

When you want to use Jira Service Desk you have to think about the projects you want to create/support there and how you want to support the customers inside your Service Desk. You can have just one project in one Jira Service Desk instance or multiple projects in one instance with different customers (1:1:n, 1:n:n). It's like multi tenancy handling...maybe you do want to have some kind of seperation between projects and customers/organziations. Every customer can be part of an organization in Service Desk, organizations can be seen as a mirror of companies of your application. You do not need to add customers to an organization, if you want to have no or just a flat hierarchy.  

For creating and receiving requests automatically you have to think about accessing the APIs...do you want to have a personal or technical user? What are the permissions you have to set....?  

In the following you will hopefully get an answer of these questions.


---


## Accessing APIs

API Access will use basic authentication which means you will always use a non technical user for accessing all APIs.  
You can also use oAuth, described in the [REST API documentation](https://developer.atlassian.com/cloud/jira/service-desk/jira-rest-api-oauth-authentication/). In this repository you will always find the requests done with basic authentication.


---



## Workflow

Functional and technical steps to achieve customer satisfaction concerning support functionality. 

We assume that we have following data: 
 - Name of the customer
 - E-Mail address of the customer
 - Company Name of the customer
 - Service Desk ID will be always the same (and will not change)


### Out of Scope

In Jira Service Desk you have different kind of request types, depending on the template of the project you choose when creating a project. Concerning the "IT Service Desk" template for example, you can choose between existing ones like "Fix an account problem", "Onboard new employes" and many more. You can also create your own custom request types manually or via API. In this repository we will use the existing template and the existing request types. It's not difficult to create custom types, you can find everything [here](https://developer.atlassian.com/cloud/jira/service-desk/rest/api-group-servicedesk/#api-rest-servicedeskapi-servicedesk-servicedeskid-requesttype-post).

### Possible workflow 


0. Not needed when we assume we have always the same  Service Desk Id but still good to know.
   We could have several service desks and maybe do want to create requests etc. in all, but just one of them. So we are calling all existing service desks and look for a specific one with a special name to receive its `internal id`.  
   [Get Specific Service Desk Id](Requests.md/#get-all-services-desks).

   ```
   function getServiceDeskId (your Service Desk name) {
      return internalServicedeskId 
   }
   ```


1. We try to check if the organization/customer exists in Jira Service Desk. If not the organization should be created and automatically added to the project.  
   [Get all organizations / Get specific organization By Id](Requests.md/#get-all-organizations)
   [Create new organzation](Requests.md/#create-organization)  
   [Add organization to specific project](Requests.md/#add-organization-to-project)

   ```
   function checkIfOrganizationExists(your organization name) {

      var exists = getAllOrganzisationAndReturnYourOne()
      If (exists) {
         take existing one
      } else {
         - create new organzation
         - add organization to specific project
      }
   }
   ```

2. We try to check if the customer exists in the organization in Jira Service Desk. If not we create the customer and add him to the organization.   
   [Get all Customers from organization / Get specific customer by E-Mail address](Requests.md/#get-customers-from-organization)    
   [Create new customer](Requests.md/#create-organization)    
   [Add customer to organziation](Requests.md/#add-customer-to-organization)

   ```
   function checkIfCustomerExists (customers email adress or name) {
      If (exists) {
         take existing one
      } else {
         create new customer
         add new customer to organzation by accountId
      }
   }

   ```


3. We have now all data we need prepared. We created/got an organization and a valid user (by get or creation of the user). 
   For creating new request tickets we always need the user id and the service desk id.  
   By using those values in the `requestParticipants` tag, we can call all requests later to filter just those tickets which are relevant to the specific user. 
   [Create Request](Requests.md/#create-request)    

   ```
   function createNewTicket(userid, serviceDeskId) {
   }
   ``` 


5. We can also get the feedback from support, if they comment the ticket, the ticket status and so on. 
   It's relevant to give the customer the feedback if somebody is already working on his problem. 
   [Get Request](Requests.md/#get-customer-request)    

   ```
   function getCustomerRequest(serviceDeskId, emailAdress/userid) {
      return status, comments, description...
   }
   ```


6. If the response from support did not help the customer he should be able to answer and ask for more help.   
   This can also be done via request on the same ticket as comment.     
   Please regard that we use the technical user for the API and in this request we have no possibility to add extra annotations/data like request particants. So in Jira Service Desk you will not see the real customer commenting but the technical user. So we have to make sure that the request will be sent from the right customer.
   [Create comment on Customer Request](Requests.md/#create-customer-request-comment)    

   ```
   function createCommentOnCustomerRequest(serviceDeskId, emailAdress/userid) {
   }
   ```