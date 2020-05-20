# HX API Documentation for Homer Technique Scores
### Section 1: Description
There are three priority collections for the HX Innovations api:
- Organizations (list of organizations)
- Products List (list of products currently being tested for their specific organization)
- Product Summary (Summary of the results tested from the product) 

### Section 2: Authentication 
There is a two step authentication process involving custom token and security token. The custom token is created based on the user UID, and the security token is created based on the custom token value. Example Below:
1. Custom Token Endpoint | GET method
`https://us-central1-hxapp-38bf8.cloudfunctions.net/getToken?uid=<YOURUID>`

  params to pass with a get command
- uid=<YOURUID>
  Response Back 
  - custom token
2. Security Token Endoint | POST Method
  `https://identitytoolkit.googleapis.com/v1/accounts:signInWithCustomToken?key=AIzaSyCtHfLNTh_mQt5YRTAol5QouEuoFWFrQyI`
  
 The payload should include the following: 
  
  ```json
  {
  "token":"<YOURCUSTOMTOKEN>",
  "returnSecureToken":true
  }
  ```
  Response Object:
  ```json
  {
  "kind": "identitytoolkit#VerifyCustomTokenResponse",
  "idToken": "<YOURSECURITYTOKEN>",
  "refreshToken": "<YOURREFRESHSECURITYTOKEN>",
  "expiresIn": "3600",
  "isNewUser": false
  } 
  ```

### Section 3: Organization, Product List, and Product Summary Collection
#### 1. Organization Collection | POST METHOD | This method contains a list of organizations that is apart of our collection. 
`https://us-central1-hxapp-38bf8.cloudfunctions.net/getOrgs`
- Payload Object: 
```json 
{
  data: {
  "getorgs": "getorgs"
  }
}
```
- Header Object for Authorization: 
```json 
{
"Authorization" : "Bearer <YOURSECURITYTOKEN>"
}
```
- Response Object:
```json 
{
    "result": [
        {
            "name": "Jaylen's Shoe Line",
            "id": "0gSOWUsfaefvsdf"
        },
        {
            "name": "Shoe Line Two",
            "id": "GyoL4sdsfewf"
        },
        {
            "name": "Company Three",
            "id": "SyXs7qwewqerw"
        },
    ]
}

```
#### 2. Product List | Post method | This method contains a list of products related to the specific organizations id

`https://us-central1-hxapp-38bf8.cloudfunctions.net/getOrgProducts`
- Payload Object: (Include organization id of the specific org 
``` json
{ "data":
 { "orgID": "0gSOWUPxdXyzLgbJ7kIM" }
}
```
- Header Object for Authorization: 
```json 
{
"Authorization" : "Bearer <YOURSECURITYTOKEN>"
}
```

- Response Object: 
``` json 
{
    "result": [
        {
            "name": "Removemetwp",
            "id": "gP6WEwyqOcJvDxJxgWqd"
        },
        {
            "name": "RemoveMe",
            "id": "r5Ea4o5XlzMvvts0k7zL"
        },
        {
            "name": "RemoveThree",
            "id": "wefrBvJlSrfZDBQY0ra7"
        }
    ]
}
```
#### 3. Product Summary | Post Method | This method contains the product summary/Homer Technique Scores for a specific product id endpoint below: 

`https://us-central1-hxapp-38bf8.cloudfunctions.net/getProductSummary`
- Payload Object: 
``` json
{ "data": {
	"shoeID":"gP6WEwyqOcJvDxJxgWqd"
	}
}
```
- Header Object for Authorization: 
```json 
{
"Authorization" : "Bearer <YOURSECURITYTOKEN>"
}
```

- Response Object: 
``` json 
{
    "result": {
        "summary": {
            "comfort": 0,
            "htScore": 0,
            "fatigue": 0,
            "testCount": 0,
            "balance": 0
        },
        "name": "Removemetwp",
        "organizationId": "0gSOWUPxdXyzLgbJ7kIM"
    }
}
```
