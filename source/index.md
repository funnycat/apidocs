---
title: API Reference

language_tabs:
  - Example: json

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Bento for Business API! You can use our API to access Bento's API endpoints. 

We have language bindings in Shell and Java! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Sessions

Sessions are used to control access and login or logout an user.

## Create a Session

> To create a new session, use this code:

```json

{
  "loginName": "example@bentoforbusiness.com",
  "password": "MyPassword1"
}
```



> The response will be a token in this format:

```json
{
  "token":"146|KYpRTwH75OMl7y0zFE_T03hEkLSIGdoSdTH0eby5cug\u003d"
}
```

Creates a new Session for an existing Business. Each Session Token is valid for 3 hours.


### HTTP Request

`POST /api/sessions`

### Attributes

Parameter | Required | Description
--------- | -------  | -----------
loginName | true     | The email you provided when signing up your business.
password  | true     | Your password


The authorization token needs to be passed on to the server as an Authorization Header, using the `Bearer` authentication type.

`Authorization: Bearer  146|KYpRTwH75OMl7y0zFE_T03hEkLSIGdoSdTH0eby5cug\u003d`

<aside class="notice">
After receiving your `token`, it must be used as an `Authorization` header for all subsequent calls.
</aside>

## Delete a Session

Deleting a session logs the user out of the api.


### HTTP Request

`DELETE /api/sessions`

You will receive a `200 OK` response from the server back but no content.


## Update Password

### HTTP Request

`PUT /api/sessions`

### Attributes

Parameter | Required | Description
--------- | -------  | -----------
loginName | true     | The email you provided when signing up your business.
password  | true     | Your password


```json

{
  "loginName": "example@bentoforbusiness.com",
  "password": "MyPassword1"
}
```



> The response will be a token in this format:

```json
{
  "token":"146|KYpRTwH75OMl7y0zFE_T03hEkLSIGdoSdTH0eby5cug\u003d"
}
```


# Business




## Get the Current Business


### HTTP Request

`GET /api/businesses/me`


This will return the current business object.


> The business Object looks like this:

```json
{
  businessId: 1,
  "additionalInfo": {
    "employeeQty": "6-10",
    "industry": "Software",
    "promoCode": "",  
  }
  "address": {
    "active": true,
    "addressType": "business",
    "city": "San Francisco",
    "state": "CA",
    "street": "300 Beale St",
    "zipCode": "94105" 
  },
  "approvalStatus": "Approved",
  "balance": 20000.0,
  "companyName": "Bento",
  "phone": "5551234567",
  "timeZone": "America/Los_Angeles"
}


```




## Update a business

### HTTP Request


`PUT /api/businesses/me`


### Attributes

Parameter    |  Description
---------    |    -----------
companyName  | The company Name
nameOnCard   | The name that appears on the 4th line of the card
phone        | The business phone number
taxId        | The Business Tax Id
businessStructure| The Business Structure (Sole_Proprietorship, Partnership, LLC, S_Corp, C_Corp, Non_Profit)
additionalInfo| An object containing additional info
address| An object containing the business Address.


### Additional Info Attributes

Parameter    |  Description
---------    |    -----------
employeeQty  | The number of Employees 
industry     | The industry of the business
promoCode    |  Promo code used during enrollment
heardBentoFrom| Where did you hear about Bento

### Address Attributes

Parameter    |  Description
---------    |    -----------
street       |  Business Street
city         |  Business City
addressAdditionals | Additional Info (Apt #, suite, etc)
state        | Business State
country      | Business Country
zipCode      | Business Zipcode


This will return the current business object.

> The business Object looks like this:

```json

{
  "businessId": 1,
  "additionalInfo": {
    "employeeQty": "6-10",
    "industry": "Software",
    "promoCode": ""  
  }, 
  "address": {
    "active": true,
    "addressType": "business",
    "city": "San Francisco",
    "state": "CA",
    "street": "300 Beale St",
    "zipCode": "94105" 
  },
  "approvalStatus": "Approved",
  "balance": 20000.0,
  "companyName": "Bento",
  "businessStructure": "Partnership",
  "phone": "5551234567",
  "nameOnCard": "BENTO FOR BUSINESS", 
  "timeZone": "America/Los_Angeles",
  "taxId": "455778888"
}


```

# Users

## Get a list of users

### HTTP Request


`GET /api/users`

Gets a list of users associated with the current business.


> Returns an array of users

```json
[
  {
    "homePhone": "5551234567",
    "address": {
      "street": "414 Brannan St.",
      "city": "San Francisco",
      "zipCode": "94107",
      "addressType": "business",
      "state": "CA",
      "active": true,
      "deleted": false
    },
    "userId": 14,
    "email": "businessowner@example.com",
    "firstName": "John",
    "lastName": "Smith",
    "phone": "4159876543",
    "birthDate": 161049600000,
    "approvalStatus": "Approved"
  }, 
  {
    "userId": 357,
    "email": "adminuser@example.com",
    "firstName": "Admin",
    "lastName": "Wong",
    "approvalStatus": "Approved"
  },
  {
    "userId": 361,
    "firstName": "Steph",
    "lastName": "Perez",
    "birthDate": 275986800000,
    "approvalStatus": "Approved"
  }
]

```

## Create a new Admin

### HTTP Request


`POST /api/users`




