<h2 id="get-all-services-desks">Get all Service Desks / Get specific Service Desk By Id</h2>

  - Request for all Service Desks
    ```
    curl --request GET \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/servicedesk' \
      --header 'Accept: application/json'
    ```

  - Repsonse for all Service Desks
    ```
    ...
    {
      "id": "1",
      "projectId": "10001",
      "projectName": "Demo desk",
      "projectKey": "DEMO",
      "_links": {
        "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/servicedesk/1"
      }
    },
    {
      "id": "2",
      "projectId": "10000",
      "projectName": "IT Service desk",
      "projectKey": "ISD",
      "_links": {
        "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/servicedesk/2"
      }
    }    
    ...
    ```

---

<h2 id="get-all-organizations">Get all organizations / Get specific organization By Id</h2>

  - Request for all organziations
    ```
    curl --request GET \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization' \
      --header 'Accept: application/json'
    ```

  - Reponse for all organziations
    ```
    ...
    {
      "id": "1",
      "name": "Company 1",
      "_links": {
        "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization/1"
      }
    },
    {
      "id": "2",
      "name": "Company 2",
      "_links": {
        "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization/2"
      }
    }    
    ...
    ``` 


---


<h2 id="create-organization">Create organization</h2>

  - Request for creating organization
    ```
    curl --request POST \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization' \
      --header 'Accept: application/json' \
      --header 'Content-Type: application/json' \
      --data '{
      "name": "Charlie Cakes 3333 Franchises"
      }'
    ```

  - Response  for creating organization
    ```
    {
      "id": "3",
      "name": "Charlie Cakes 3333 Franchises",
      "_links": {
        "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization/3"
      }
    }
    ``` 


---


<h2 id="add-organization-to-project">Add Organization to project</h2>

  - Request for adding organization to project
    ```
    curl --request POST \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/servicedesk/1/organization' \
      --header 'Content-Type: application/json' \
      --data '{
      "organizationId": 3
      }'
    ```

  - Response  for creating organization: Response Code 204


---


<h2 id="get-customers-from-organization">Get all Customers from organization / Get specific customer by E-Mail address</h2>

  - Request for getting all customers
    ```
    curl --request GET \
      --url 'https://mrmyiagi.atlassian.net/servicedeskapi/organization/3/user' \
      --header 'Accept: application/json'
    ```

  - Response for getting all customers - no "first" or any customers available
    ```
    {
      "size": 0,
      "start": 0,
      "limit": 50,
      "isLastPage": true,
      "_links": {
          "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization/3/user",
          "base": "https://mrmyiagi.atlassian.net",
          "context": ""
      },
      "values": []
    }
    ```
  - Response for getting all customers - customers already added and available
    ```
    {
      "size": 0,
      "start": 0,
      "limit": 50,
      "isLastPage": true,
      "_links": {
          "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization/3/user",
          "base": "https://mrmyiagi.atlassian.net",
          "context": ""
      },
      "values": [
        {
          "accountId": "qm:1dc3818c-9fe1-4abf-a66a-f48e41eb4b49:99b430e4-c46f-483d-b11a-c51f04485115",
          "emailAddress": "snoopy@snoopyasdasd.com",
          "displayName": "snoopy@snoopyasdasd.com",
          "active": true,
          "timeZone": "Europe/Berlin",
          "_links": {
              "jiraRest": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=qm%3A1dc3818c-9fe1-4abf-a66a-f48e41eb4b49%3A99b430e4-c46f-483d-b11a-c51f04485115",
              "avatarUrls": {
                  "48x48": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png",
                  "24x24": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png",
                  "16x16": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png",
                  "32x32": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png"
              },
              "self": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=qm%3A1dc3818c-9fe1-4abf-a66a-f48e41eb4b49%3A99b430e4-c46f-483d-b11a-c51f04485115"
            }
        }        
      ]
    }
    ```


---


<h2 id="create-customer">Create customer</h2>

  - Request for creating customer
    ```
    curl --request POST \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/customer' \
      --header 'Accept: application/json' \
      --header 'Content-Type: application/json' \
      --data '{
      "displayName": "Fred F. User 222",
      "email": "fred222@example.com"
      }'
    ```
  
  - Response for creating customer
    ```
    {
      "accountId": "qm:1dc3818c-9fe1-4abf-a66a-f48e41eb4b49:402a5dd8-5d16-4a00-b401-301de53f0f56",
      "emailAddress": "fred222@example.com",
      "displayName": "Fred F. User 222",
      "active": true,
      "timeZone": "Europe/Berlin",
      "_links": {
          "jiraRest": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=qm%3A1dc3818c-9fe1-4abf-a66a-f48e41eb4b49%3A402a5dd8-5d16-4a00-b401-301de53f0f56",
          "avatarUrls": {
              "48x48": "https://avatar-management.services.atlassian.com/default/48",
              "24x24": "https://avatar-management.services.atlassian.com/default/24",
              "16x16": "https://avatar-management.services.atlassian.com/default/16",
              "32x32": "https://avatar-management.services.atlassian.com/default/32"
          },
          "self": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=qm%3A1dc3818c-9fe1-4abf-a66a-f48e41eb4b49%3A402a5dd8-5d16-4a00-b401-301de53f0f56"
      }
    }
    ``` 


---


<h2 id="add-customer-to-organization">Add customer to organziation</h2>

  - Request for adding customer to organization - Response Code 204
    ```
    curl --request POST \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/organization/{organizationId}/user' \
      --header 'Content-Type: application/json' \
      --data '{
      "accountIds": [
        "qm:1dc3818c-9fe1-4abf-a66a-f48e41eb4b49:402a5dd8-5d16-4a00-b401-301de53f0f56"
      ],
      "usernames": []
    }'
    ```

  - Response for adding customer to organization - Response Code 204


---


<h2 id="create-request">Create Request</h2>

  - Request for creating new customer request
  ```
    curl --request POST \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/request' \
      --header 'Accept: application/json' \
      --header 'Content-Type: application/json' \
      --data '{
      "requestParticipants": [
        "qm:1dc3818c-9fe1-4abf-a66a-f48e41eb4b49:402a5dd8-5d16-4a00-b401-301de53f0f56"
      ],
      "serviceDeskId": "2",
      "requestTypeId": "9",
      "requestFieldValues": {
        "summary": "Request JSD help via REST",
        "description": "I need a new *mouse* for my Mac"
      }
    }'
  ```

  - Response for creating new customer request
  ```
  {
    "_expands": [
        "participant",
        "status",
        "sla",
        "requestType",
        "serviceDesk",
        "attachment",
        "action",
        "comment"
    ],
    "issueId": "10013",
    "issueKey": "ISD-2",
    "requestTypeId": "9",
    "serviceDeskId": "2",
    "createdDate": {
        "iso8601": "2020-08-07T15:41:47+0200",
        "jira": "2020-08-07T15:41:47.686+0200",
        "friendly": "Today 3:41 PM",
        "epochMillis": 1596807707686
    },
    "reporter": {
        "accountId": "5b9f8ca5990ff108598595d3",
        "emailAddress": "marcel.schmitt.2012@gmail.com",
        "displayName": "Marcel Schmitt",
        "active": true,
        "timeZone": "Europe/Berlin",
        "_links": {
            "jiraRest": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=5b9f8ca5990ff108598595d3",
            "avatarUrls": {
                "48x48": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png",
                "24x24": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png",
                "16x16": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png",
                "32x32": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png"
            },
            "self": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=5b9f8ca5990ff108598595d3"
        }
    },
    "requestFieldValues": [
        {
            "fieldId": "summary",
            "label": "Summary",
            "value": "Request JSD help via REST"
        },
        {
            "fieldId": "description",
            "label": "Description",
            "value": "I need a new *mouse* for my Mac",
            "renderedValue": {
                "html": "<p>I need a new <b>mouse</b> for my Mac</p>"
            }
        },
        {
            "fieldId": "attachment",
            "label": "Attachment",
            "value": []
        }
    ],
    "currentStatus": {
        "status": "Waiting for support",
        "statusCategory": "INDETERMINATE",
        "statusDate": {
            "iso8601": "2020-08-07T15:41:47+0200",
            "jira": "2020-08-07T15:41:47.686+0200",
            "friendly": "Today 3:41 PM",
            "epochMillis": 1596807707686
        }
    },
    "_links": {
        "jiraRest": "https://mrmyiagi.atlassian.net/rest/api/2/issue/10013",
        "web": "https://mrmyiagi.atlassian.net/servicedesk/customer/portal/2/ISD-2",
        "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/request/10013"
    }
  }
  ```

---


<h2 id="get-customer-request">Get Customer Request</h2>

  - Request for getting customer request
    ```
    curl --request GET \
      --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/request?expand=participant&serviceDeskId=2' \
      --header 'Accept: application/json'
    ```

  - Response for getting customer request
    ```
    {
    "_expands": [
        "participant",
        "status",
        "sla",
        "requestType",
        "serviceDesk",
        "attachment",
        "action",
        "comment"
    ],
    "size": 7,
    "start": 0,
    "limit": 50,
    "isLastPage": true,
    "_links": {
        "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/request?expand=participant&serviceDeskId=2",
        "base": "https://mrmyiagi.atlassian.net",
        "context": ""
    },
    "values": [
{
            "_expands": [
                "participant",
                "status",
                "sla",
                "requestType",
                "serviceDesk",
                "attachment",
                "action",
                "comment"
            ],
            "issueId": "10018",
            "issueKey": "ISD-7",
            "requestTypeId": "9",
            "serviceDeskId": "2",
            "createdDate": {
                "iso8601": "2020-08-11T15:51:42+0200",
                "jira": "2020-08-11T15:51:42.309+0200",
                "friendly": "Today 3:51 PM",
                "epochMillis": 1597153902309
            },
            "reporter": {
                "accountId": "5b9f8ca5990ff108598595d3",
                "emailAddress": "marcel.schmitt.2012@gmail.com",
                "displayName": "Marcel Schmitt",
                "active": true,
                "timeZone": "Europe/Berlin",
                "_links": {
                    "jiraRest": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=5b9f8ca5990ff108598595d3",
                    "avatarUrls": {
                        "48x48": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png",
                        "24x24": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png",
                        "16x16": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png",
                        "32x32": "https://secure.gravatar.com/avatar/799f8651b94300779b30532516047c97?d=https%3A%2F%2Favatar-management--avatars.us-west-2.prod.public.atl-paas.net%2Finitials%2FMS-0.png"
                    },
                    "self": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=5b9f8ca5990ff108598595d3"
                }
            },
            "requestFieldValues": [
                {
                    "fieldId": "summary",
                    "label": "Summary",
                    "value": "something is wrong with the api"
                },
                {
                    "fieldId": "description",
                    "label": "Description",
                    "value": "help me! ",
                    "renderedValue": {
                        "html": "<p>help me! </p>"
                    }
                },
                {
                    "fieldId": "attachment",
                    "label": "Attachment",
                    "value": []
                }
            ],
            "currentStatus": {
                "status": "Waiting for support",
                "statusCategory": "INDETERMINATE",
                "statusDate": {
                    "iso8601": "2020-08-11T15:51:42+0200",
                    "jira": "2020-08-11T15:51:42.309+0200",
                    "friendly": "Today 3:51 PM",
                    "epochMillis": 1597153902309
                }
            },
            "participants": {
                "size": 1,
                "start": 0,
                "limit": 50,
                "isLastPage": true,
                "_links": {
                    "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/request/ISD-7/participant",
                    "base": "https://mrmyiagi.atlassian.net",
                    "context": ""
                },
                "values": [
                    {
                        "accountId": "qm:1dc3818c-9fe1-4abf-a66a-f48e41eb4b49:84a9279b-010e-4878-8758-c1b80d51c0f0",
                        "emailAddress": "marcel.mj.schmitt@web.de",
                        "displayName": "Marcel Schmitt",
                        "active": true,
                        "timeZone": "Europe/Berlin",
                        "_links": {
                            "jiraRest": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=qm%3A1dc3818c-9fe1-4abf-a66a-f48e41eb4b49%3A84a9279b-010e-4878-8758-c1b80d51c0f0",
                            "avatarUrls": {
                                "48x48": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png",
                                "24x24": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png",
                                "16x16": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png",
                                "32x32": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/default-avatar.png"
                            },
                            "self": "https://mrmyiagi.atlassian.net/rest/api/2/user?accountId=qm%3A1dc3818c-9fe1-4abf-a66a-f48e41eb4b49%3A84a9279b-010e-4878-8758-c1b80d51c0f0"
                        }
                    }
                ]
            },
            "_links": {
                "jiraRest": "https://mrmyiagi.atlassian.net/rest/api/2/issue/10018",
                "web": "https://mrmyiagi.atlassian.net/servicedesk/customer/portal/2/ISD-7",
                "self": "https://mrmyiagi.atlassian.net/rest/servicedeskapi/request/10018"
            }
        }
      ]
    }
    ```  