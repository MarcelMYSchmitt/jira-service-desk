
### Get all Service Desks

```
curl --request GET \
  --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/servicedesk' \
  --header 'Accept: application/json'
```

Returns all projects with the internal and project sepcific ids such as the project name and the project key. 

---

### Get Service Desk by internal ID

```
curl --request GET \
  --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/servicedesk/3' \
  --header 'Accept: application/json'
```

For example: 
 - projectName: TestProject
 - projectKey: TP
 - projectId: 10002
 - internalId: 3

---

### Get all customers from specific project

```
curl --request GET \
  --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/servicedesk/3/customer' \
  --header 'Accept: application/json'
```

Returns all customers from the specific Project `Test Project`with teir internal ids, email adresses, display names, and their current status (active or not).

---

## Get specifc customer from specific project


For example: 
- accountId: 5b9f8ca5990ff108598595d3
- emailAddress: marcel.schmitt.2012@gmail.com
- displayName: Marcel Schmitt
- active: true


---

### Add customer

```
curl --request POST \
  --url 'https://mrmyiagi.atlassian.net/rest/servicedeskapi/customer' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{
  "displayName": "Marcel Schmitt",
  "email": "marcel.schmitt.2012@gmail.com"
}'
```
