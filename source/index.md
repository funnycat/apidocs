---
title: API Reference

language_tabs:
  - Example: json

toc_footers:
  - Questions? Click <a href="mailto:api@bentoforbusiness.com">Here</a>

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
  "businessId": 1,
  "additionalInfo": {
    "employeeQty": "6-10",
    "industry": "Software",
    "promoCode": ""
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


## Get a specific User


### HTTP Request


`GET /api/users/<userId>`

<aside class="notice">You can use "me" as userId to get information about the current user.</aside>

```json
{
  "userId": 586,
  "email": "someone@somplace.com",
  "firstName": "BUSINESS",
  "lastName": "OWNER",
  "phone": "5312123132",
  "birthDate": 276073200000
}

```

## Create a new Admin

### HTTP Request


`POST /api/users`

Creates a new Admin user


### Attributes

Parameter    |  Description
---------    |    -----------
birthDate    |  The date of birth of the admin (Unix Epoch time)
email        |  The admin's email address
fistName     |  First name
lastName     |  Last name
phone        |  Admin's mobile phone
type         |  Should be set to "BusinessAdmin"

```json

{
    "birthDate": 276073200000,
    "email": "john@somecompany.com",
    "firstName": "John",
    "lastName": "Smith",
    "phone": "4567891234",
    "type": "BusinessAdmin"
}

```

## Update an User

### HTTP Request


`PUT /api/users/<userId>`


<aside class="notice">You can use "me" as userId to get information about the current user.</aside>

Updates an User


### Attributes

Parameter    |  Description
---------    |    -----------
address      |  An object containing the address of the user
fistName     |  First name
lastName     |  Last name
homePhone    |  User's home phone
birthDate    | Date of birth for the user
phone        | User's mobile phone



### Address Attributes

Parameter    |  Description
---------    |    -----------
street       |  User Street
city         |  User City
addressAdditionals | Additional Info (Apt #, suite, etc)
state        | User State
country      | User Country
zipCode      | User Zipcode

```json

{
    "address": {
        "city": "San Francisco",
        "country": "USA",
        "state": "CA",
        "street": "1 My way",
        "zipCode": "94105"
    },
    "birthDate": 276073200000,
    "firstName": "JOHN",
    "homePhone": "5564564564",
    "lastName": "SMITH",
    "phone": "5312123132"
}

```

## Delete an user

### Http Request

`DELETE /api/users/<userId>`

Deletes an user. You should get an 200 OK back but no content when the user is deleted.

<aside class="notice">You can use "me" as userId to get information about the current user.</aside>


# Cards

## Get Cards

Gets all cards for the business

### HTTP Request

`GET /api/cards`

> Sample Json Response

```json
[
  {
    "cardId": 356,
    "user": {
      "homePhone": "5564564564",
      "address": {
        "id": 200,
        "street": "1 My way",
        "city": "San Francisco",
        "country": "USA",
        "zipCode": "94105",
        "addressType": "employee",
        "state": "CA",
        "active": false,
        "deleted": false
      },
      "userId": 586,
      "email": "someone@bentoforbusiness.com",
      "firstName": "JOHN",
      "lastName": "SMITH",
      "phone": "5312123132",
      "birthDate": 276073200000,
      "deleted": false,
      "created": 1447791025000,
      "approvalStatus": "Review"
    },
    "type": "BusinessOwnerCard",
    "lifecycleStatus": "NOT_ISSUED_YET",
    "status": "TURNED_OFF",
    "alias": "JOHN SMITH",
    "spendingLimit": {
      "amount": 25000,
      "period": "Day",
      "active": false
    },
    "allowedCategories": [
      {
        "transactionCategoryId": 1,
        "name": "Fuel Pumps",
        "type": "SPENDING",
        "description": "Automated Fuel Dispensers Only"
      },
      {
        "transactionCategoryId": 2,
        "name": "Gas Stations",
        "type": "SPENDING",
        "description": "Gas stations including convenience stores at gas stations"
      },
      {
        "transactionCategoryId": 3,
        "name": "Travel & Transportation",
        "type": "SPENDING",
        "description": "Rental Cars, Airlines, Public Transit, Etc."
      },
      {
        "transactionCategoryId": 4,
        "name": "Home, Garden Supply & Service",
        "type": "SPENDING",
        "description": "Hardware stores, plumbers, landscape businesses, lumber, parts, and equipment"
      },
      {
        "transactionCategoryId": 5,
        "name": "Home Furnishing",
        "type": "SPENDING",
        "description": "Furniture, Draperies, Flooring and Speciality"
      },
      {
        "transactionCategoryId": 6,
        "name": "Wholesale Clubs & Office Supplies",
        "type": "SPENDING",
        "description": "Wholesale club stores, office supplies, stationery stores"
      },
      {
        "transactionCategoryId": 7,
        "name": "Business Services",
        "type": "SPENDING",
        "description": "Photography, Secretarial, Computer Consulting, etc."
      },
      {
        "transactionCategoryId": 8,
        "name": "Professional Services",
        "type": "SPENDING",
        "description": "Insurance, Legal, Real Estate, Doctors, Medical, etc."
      },
      {
        "transactionCategoryId": 9,
        "name": "Repair Services",
        "type": "SPENDING",
        "description": "Autobody, auto painting, electronics and equipment repair, etc."
      },
      {
        "transactionCategoryId": 10,
        "name": "Personal Services",
        "type": "SPENDING",
        "description": "Laundries, Dry Cleaners, Barbers, Hairdressers, Shoe Repair,e tc."
      },
      {
        "transactionCategoryId": 11,
        "name": "Retail and Miscellaneous Stores",
        "type": "SPENDING",
        "description": "Clothing, Variety, Sporting Goods, etc."
      },
      {
        "transactionCategoryId": 12,
        "name": "Wholesale Trade",
        "type": "SPENDING",
        "description": "Office Furniture, Computers, Chemical Products, etc."
      },
      {
        "transactionCategoryId": 13,
        "name": "Telecom, Internet & Utilities",
        "type": "SPENDING",
        "description": "Phone, Cable, Internet and other utlities"
      },
      {
        "transactionCategoryId": 14,
        "name": "Restaurants",
        "type": "SPENDING",
        "description": "Restaurants"
      },
      {
        "transactionCategoryId": 15,
        "name": "Automobiles and Vehicles",
        "type": "SPENDING",
        "description": "Auto, Motorcycle, RV, and Boat Sales, Auto Parts, etc."
      },
      {
        "transactionCategoryId": 16,
        "name": "Financial Services",
        "type": "SPENDING",
        "description": "Money order, OTC Cash Disbursement, etc."
      },
      {
        "transactionCategoryId": 17,
        "name": "Amusement and Entertainment",
        "type": "SPENDING",
        "description": "Movie Theaters, Pool Halls, Bowling Alleys, etc."
      },
      {
        "transactionCategoryId": 18,
        "name": "Associations",
        "type": "SPENDING",
        "description": "Religious, Charitable, Social, and Membership Associations"
      },
      {
        "transactionCategoryId": 19,
        "name": "Liquor and Alcohol Stores",
        "type": "SPENDING",
        "description": "Liquor Stores"
      },
      {
        "transactionCategoryId": 20,
        "name": "Education",
        "type": "SPENDING",
        "description": "Universities, Trade Schools"
      },
      {
        "transactionCategoryId": 21,
        "name": "Government Services",
        "type": "SPENDING",
        "description": "Fines, Taxes, Government Services, Court, Bail, etc."
      },
      {
        "transactionCategoryId": 22,
        "name": "Mail Phone Order",
        "type": "SPENDING",
        "description": "Direct Marketing and Door-to-Door"
      }
    ],
    "allowedCategoriesActive": false,
    "internalAllowedDays": 127,
    "allowedDays": [
      "MONDAY",
      "TUESDAY",
      "WEDNESDAY",
      "THURSDAY",
      "FRIDAY",
      "SATURDAY",
      "SUNDAY"
    ],
    "allowedDaysActive": false
  }
]

```


## Get a specific card

### HTTP Request

`GET /api/cards/<cardId>`

```json

{
  "cardId": 356,
  "user": {
    "homePhone": "5564564564",
    "address": {
      "id": 200,
      "street": "1 My way",
      "city": "San Francisco",
      "country": "USA",
      "zipCode": "94105",
      "addressType": "employee",
      "state": "CA",
      "active": false,
      "deleted": false
    },
    "userId": 586,
    "email": "john@somecompany.com",
    "firstName": "JOHN ",
    "lastName": "SMITH",
    "phone": "5312123132",
    "birthDate": 276073200000,
    "deleted": false,
    "created": 1447791025000,
    "approvalStatus": "Review"
  },
  "type": "BusinessOwnerCard",
  "lifecycleStatus": "NOT_ISSUED_YET",
  "status": "TURNED_OFF",
  "alias": "JOHN SMITH",
  "spendingLimit": {
    "amount": 25000,
    "period": "Day",
    "active": false
  },
  "allowedCategories": [
    {
      "transactionCategoryId": 1,
      "name": "Fuel Pumps",
      "type": "SPENDING",
      "description": "Automated Fuel Dispensers Only"
    },
    {
      "transactionCategoryId": 2,
      "name": "Gas Stations",
      "type": "SPENDING",
      "description": "Gas stations including convenience stores at gas stations"
    },
    {
      "transactionCategoryId": 3,
      "name": "Travel & Transportation",
      "type": "SPENDING",
      "description": "Rental Cars, Airlines, Public Transit, Etc."
    },
    {
      "transactionCategoryId": 4,
      "name": "Home, Garden Supply & Service",
      "type": "SPENDING",
      "description": "Hardware stores, plumbers, landscape businesses, lumber, parts, and equipment"
    },
    {
      "transactionCategoryId": 5,
      "name": "Home Furnishing",
      "type": "SPENDING",
      "description": "Furniture, Draperies, Flooring and Speciality"
    },
    {
      "transactionCategoryId": 6,
      "name": "Wholesale Clubs & Office Supplies",
      "type": "SPENDING",
      "description": "Wholesale club stores, office supplies, stationery stores"
    },
    {
      "transactionCategoryId": 7,
      "name": "Business Services",
      "type": "SPENDING",
      "description": "Photography, Secretarial, Computer Consulting, etc."
    },
    {
      "transactionCategoryId": 8,
      "name": "Professional Services",
      "type": "SPENDING",
      "description": "Insurance, Legal, Real Estate, Doctors, Medical, etc."
    },
    {
      "transactionCategoryId": 9,
      "name": "Repair Services",
      "type": "SPENDING",
      "description": "Autobody, auto painting, electronics and equipment repair, etc."
    },
    {
      "transactionCategoryId": 10,
      "name": "Personal Services",
      "type": "SPENDING",
      "description": "Laundries, Dry Cleaners, Barbers, Hairdressers, Shoe Repair,e tc."
    },
    {
      "transactionCategoryId": 11,
      "name": "Retail and Miscellaneous Stores",
      "type": "SPENDING",
      "description": "Clothing, Variety, Sporting Goods, etc."
    },
    {
      "transactionCategoryId": 12,
      "name": "Wholesale Trade",
      "type": "SPENDING",
      "description": "Office Furniture, Computers, Chemical Products, etc."
    },
    {
      "transactionCategoryId": 13,
      "name": "Telecom, Internet & Utilities",
      "type": "SPENDING",
      "description": "Phone, Cable, Internet and other utlities"
    },
    {
      "transactionCategoryId": 14,
      "name": "Restaurants",
      "type": "SPENDING",
      "description": "Restaurants"
    },
    {
      "transactionCategoryId": 15,
      "name": "Automobiles and Vehicles",
      "type": "SPENDING",
      "description": "Auto, Motorcycle, RV, and Boat Sales, Auto Parts, etc."
    },
    {
      "transactionCategoryId": 16,
      "name": "Financial Services",
      "type": "SPENDING",
      "description": "Money order, OTC Cash Disbursement, etc."
    },
    {
      "transactionCategoryId": 17,
      "name": "Amusement and Entertainment",
      "type": "SPENDING",
      "description": "Movie Theaters, Pool Halls, Bowling Alleys, etc."
    },
    {
      "transactionCategoryId": 18,
      "name": "Associations",
      "type": "SPENDING",
      "description": "Religious, Charitable, Social, and Membership Associations"
    },
    {
      "transactionCategoryId": 19,
      "name": "Liquor and Alcohol Stores",
      "type": "SPENDING",
      "description": "Liquor Stores"
    },
    {
      "transactionCategoryId": 20,
      "name": "Education",
      "type": "SPENDING",
      "description": "Universities, Trade Schools"
    },
    {
      "transactionCategoryId": 21,
      "name": "Government Services",
      "type": "SPENDING",
      "description": "Fines, Taxes, Government Services, Court, Bail, etc."
    },
    {
      "transactionCategoryId": 22,
      "name": "Mail Phone Order",
      "type": "SPENDING",
      "description": "Direct Marketing and Door-to-Door"
    }
  ],
  "allowedCategoriesActive": false,
  "internalAllowedDays": 127,
  "allowedDays": [
    "MONDAY",
    "TUESDAY",
    "WEDNESDAY",
    "THURSDAY",
    "FRIDAY",
    "SATURDAY",
    "SUNDAY"
  ],
  "allowedDaysActive": false,
  "createdOn": 1447791027000,
  "updatedOn": 1447791027000
}


```

## Create a card

Creates a new Card. 
  You will have to specify if you want an utility card or an employee card

### HTTP Request

`POST /cards`


### Attributes

Parameter    |  Description
---------    |    -----------
type         |  Either `EmployeeCard` or `CategoryCard`
allowedCategories | an array of allowedCategories
allowedCategoriesActive | boolean indicating if the allowed categories control is active
allowedDays | an array of allowed days [MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY]
allowedDaysActive | boolean indicating if the allowed days control is active
spendingLimit | an object controlling the spending limit
user | Used only on employee cards - An user object 
alias | Used only on utility card - The alias of the card.



### SpendingLimit Attributes

Parameter    |  Description
---------    |    -----------
active | boolean to enable or disable the control
amount | The limit amount
period | Day, Week or Month



### User Attributes

Parameter    |  Description
---------    |    -----------
firstName    | First name of employee
lastName     | Last name of employee
birthDate    | Birth date of employee (Unix Epoch)
phone        | Employee's phone number
email        | Employee's email



> Example of creating an employee Card with limits

```json
{
    "allowedCategories": [
        {
            "transactionCategoryId": 2
        },
        {
            "transactionCategoryId": 3
        }
    ],
    "allowedCategoriesActive": true,
    "allowedDays": [
        "MONDAY",
        "WEDNESDAY",
        "FRIDAY"
    ],
    "allowedDaysActive": true,
    "spendingLimit": {
        "active": true,
        "amount": 100,
        "period": "Month"
    },
    "type": "EmployeeCard",
    "user": {
        "birthDate": 276073200000,
        "email": "employee@somecompany.com",
        "firstName": "EMPLOYEE",
        "lastName": "NAME",
        "phone": "4564564456"
    }
}

```

> Example of creating an utility card with limits

```json

{
    "alias": "NICKNAME",
    "allowedCategories": [],
    "allowedDays": [
        "TUESDAY",
        "FRIDAY"
    ],
    "allowedDaysActive": true,
    "spendingLimit": {
        "active": true,
        "amount": 100,
        "period": "Week"
    },
    "type": "CategoryCard"
}


```


## Activate a card

Activates a card for the first time

### HTTP Request

`POST /cards/<cardId>/activation`

### Attributes

Parameter    |  Description
---------    |    -----------
lastFour     |  The last four numbers of the card

```json

  {"lastFour": 1243}

```


## Reissue a card

### HTTP Request

`POST /cards/<cardId>/reissue`

The response of this call will be the new card thas has been issued.

## Update a card

### HTTP Request

`PUT /cards/<cardId>`


> Example of updating an employee card


```json
{
    "allowedCategories": [
        {
 
            "transactionCategoryId": 5,
        },
        {
            "transactionCategoryId": 13,
        },
    ],
    "allowedDays": [
        "MONDAY",
        "WEDNESDAY",
        "FRIDAY"
    ],
    "allowedDaysActive": true,
    "spendingLimit": {
        "active": true,
        "amount": 100,
        "period": "Month"
    },
    "type": "EmployeeCard",
    "user": {
        "birthDate": 276073200000,
        "email": "employee2@somecompany.com",
        "firstName": "EMPLOYEE",
        "lastName": "NAME",
        "phone": "4564564456",
    }
}

```

> Example of updating an utility card

```json

{
    "allowedDays": [
        "TUESDAY",
        "FRIDAY",
        "THURSDAY"
    ],
    "allowedDaysActive": true,
    "spendingLimit": {
        "active": true,
        "amount": 150,
        "period": "Month"
    }
}

```

## Delete a Card

Deletes a card

### HTTP Request 

`DELETE /api/cards/<cardId>`

You will get a 200 OK Response with the deleted card as an object.

# Funding

## List Funding Sources

### HTTP Request

`GET /api/fundingsources`



> Example of a response of an array of FundingSources

```json

[
    {
        "autoReloads": [
            {
                "active": true,
                "amount": 5000.0,
                "autoReloadId": 6,
                "bentoType": "com.bentoforbusiness.entity.funding.TemporalAutoReload",
                "period": "WEEKLY",
                "timeInterval": 2,
                "updatedDate": 1447465924000
            },
            {
                "active": false,
                "amount": 1000.0,
                "autoReloadId": 73,
                "bentoType": "com.bentoforbusiness.entity.funding.BalanceAutoReload",
                "threshold": 1000.0,
                "updatedDate": 1447271882000
            }
        ],
        "bentoType": "com.bentoforbusiness.entity.funding.FundingSource",        
        "fundingSourceId": 41,
        "name": "Account : 3453",
        "serviceClassName": "com.bentoforbusiness.integrations.marqeta.fundingsources.MarqetaFundingSourceService",
        "status": "ACTIVE"
    }
]
```


## Get a funding source

### HTTP Request

`GET /api/fundingsources/<fundingSourceId>`


<aside class="notice">
You can use `default` as the fundingSourceId to get the default funding source.
</aside>

> Example of a response of a fundingsource

```json

{
        "autoReloads": [
            {
                "active": true,
                "amount": 5000.0,
                "autoReloadId": 6,
                "bentoType": "com.bentoforbusiness.entity.funding.TemporalAutoReload",
                "period": "WEEKLY",
                "timeInterval": 2,
                "updatedDate": 1447465924000
            },
            {
                "active": false,
                "amount": 1000.0,
                "autoReloadId": 73,
                "bentoType": "com.bentoforbusiness.entity.funding.BalanceAutoReload",
                "threshold": 1000.0,
                "updatedDate": 1447271882000
            }
        ],
        "bentoType": "com.bentoforbusiness.entity.funding.FundingSource",        
        "fundingSourceId": 41,
        "name": "Account : 3453",
        "serviceClassName": "com.bentoforbusiness.integrations.marqeta.fundingsources.MarqetaFundingSourceService",
        "status": "ACTIVE"
    }

```

## Create a Funding Source

Creates a new funding source

### HTTP Request

`POST /api/fundingsources`

### Attributes

Parameter    |  Description
---------    |    -----------
createData  |  Data to be passed to the funding source service
name  | The name of this fundingsource
service | The service that you are using to load funds. 


### Services Supported

The only supported funding source is:

com.bentoforbusiness.integrations.marqeta.fundingsources.MarqetaFundingSourceService 


### CreateData Attributes

Parameter    |  Description
---------    |    -----------
account_number | The account number
account_type | the account type
routing_number | the routing number 


<aside class="notice">Note the format of the fields on createData is diffenrent because is passed on to the provider.</aside>




```json

{
    "createData": {
        "account_number": "54564646",
        "account_type": "Checking",
        "routing_number": "021000021"
    },
    "name": "TEST",
    "service": "com.bentoforbusiness.integrations.marqeta.fundingsources.MarqetaFundingSourceService"
}

```


## Verify Funding Source

Verifies that funding source and make it available to use.

### HTTP Request

`PUT /api/fundingsources/<fundingSourceId>/verifyMarqeta`

### Attributes

Parameter   |  Description
----- |  -----
amount1 | The first amount
amount2 | The second amount

```json
  {
    "amount1": 0.02,
    "amount2": 0.35
  }
  

```

## Delete Funding Source

Deletes a funding Source

### HTTP Request

`DELETE /api/fundingsources/<fundingsourceId>`

The response will be a 200 OK with the deleted object as content.

## Load Money

Loads money into your bento account

### HTTP Request

`POST /api/fundingsources/<fundingsourceId>/fundingTransactions`

### Attributes

Parameter  | Description
----- | -----
amount  | The amount to load


```json

  {
    "amount":1000.0
  }

```

## List Loads

List loads for a specific fundingsource or for the business

### HTTP Request

`GET /api/fundingsources/<fundingsourceId>/fundingTransactions`

`GET /api/fundingsources/fundingTransactions`



### Attributes

Field | Description
------|------
amount| The amount loaded
availableBy | The date that this load is going to be available
fundingTransactionId | The id of the load
status | Status of Load (PENDING, PROCESSING, NOT_PROCESSED, CANCELED)
transactionDate | The date the load initiated
changeStatusDate | The date of the last status change



```json

[
    {
        "amount": 5000.0,
        "availableBy": 1448035201000,
        "changeStatusDate": 1447789402000,
        "fundingTransactionId": 2827,
        "status": "PROCESSING",
        "transactionDate": 1447789401000
    },
    {
        "amount": 2500.0,
        "availableBy": 1447689615000,
        "changeStatusDate": 1447689615000,
        "fundingTransactionId": 2686,
        "status": "PROCESSED",
        "transactionDate": 1447113616000
    }
]

```




## Get an Autoreload

### HTTP Request

`GET /api/fundingsources/<fundingSourceId>/autoreloads`

<aside class="notice">
You can use `default` as the fundingSourceId to get the default funding source.
</aside>

> Example of a response of an autoreload



```json
[
    {
        "active": true,
        "amount": 5000.0,
        "autoReloadId": 6,
        "bentoType": "com.bentoforbusiness.entity.funding.TemporalAutoReload",
        "period": "WEEKLY",
        "timeInterval": 2,
        "updatedDate": 1447465924000
    },
    {
        "active": false,
        "amount": 1000.0,
        "autoReloadId": 73,
        "bentoType": "com.bentoforbusiness.entity.funding.BalanceAutoReload",
        "threshold": 1000.0,
        "updatedDate": 1447271882000
    }
]

```

## Create an Autoreload

### HTTP Request

`POST /api/fundingsources/<fundingsourceId>/autoreloads`

Creates a new autoreload.

There are two types of autoreloads with different fields on them.

### Temporal AutoReload Attributes

Parameter    |  Description
---------    |    -----------
active    |  Is this autoreload active
amount    |  The amount to be reload
bentoType  | com.bentoforbusiness.entity.funding.TemporalAutoReload
period | DAILY, WEEKLY, MONTHLY
timeInterval | day to trigger the reload


timeInterval has the following format:

### timeInterval 

Value  | Meaning
---- | ----
DAILY | always 1.
WEEKLY | 1 - Sun, 2 - Mon, 3 - Tue, 4 - Wed, 5 - Thu, 6 - Fri, 7 - Sat
MONTHLY | The day of the month to trigger.


### Balance Autoreload Attributes

Parameter    |  Description
---------    |    -----------
active    |  Is this autoreload active
amount    |  The amount to be reload
bentoType  | com.bentoforbusiness.entity.funding.BalanceAutoReload
threshold | when to trigger the reload.

> Temporal Autoreload

```json 

{
    "active": true,
    "amount": 10,
    "bentoType": "com.bentoforbusiness.entity.funding.TemporalAutoReload",
    "period": "WEEKLY",
    "timeInterval": 1
}

```

> Balance Autoreload


```json
{
    "active": true,
    "amount": 10,
    "bentoType": "com.bentoforbusiness.entity.funding.BalanceAutoReload",
    "threshold": 10
}

```

## Update an autoreload


### HTTP Request

`PUT /api/fundingsources/<fundingSourceId>/autoreloads/<autoreloadId>`

There are two types of autoreloads with different fields on them.

### Temporal AutoReload Attributes

Parameter    |  Description
---------    |    -----------
active    |  Is this autoreload active
amount    |  The amount to be reload
bentoType  | com.bentoforbusiness.entity.funding.TemporalAutoReload
period | DAILY, WEEKLY, MONTHLY
timeInterval | day to trigger the reload


timeInterval has the following format:

### timeInterval 

Value  | Meaning
---- | ----
DAILY | always 1.
WEEKLY | 1 - Sun, 2 - Mon, 3 - Tue, 4 - Wed, 5 - Thu, 6 - Fri, 7 - Sat
MONTHLY | The day of the month to trigger.


### Balance Autoreload Attributes

Parameter    |  Description
---------    |    -----------
active    |  Is this autoreload active
amount    |  The amount to be reload
bentoType  | com.bentoforbusiness.entity.funding.BalanceAutoReload
threshold | when to trigger the reload.

> Temporal Autoreload

```json 

{
    "active": true,
    "amount": 10,
    "bentoType": "com.bentoforbusiness.entity.funding.TemporalAutoReload",
    "period": "WEEKLY",
    "timeInterval": 1
}

```

> Balance Autoreload


```json
{
    "active": true,
    "amount": 10,
    "bentoType": "com.bentoforbusiness.entity.funding.BalanceAutoReload",
    "threshold": 10
}

```

# Transactions

## Get Transaction

Gets a specific transaction

### HTTP Request

`GET /api/transactions/<transactionId>`

### Fields

Field | Description
---- | -----
amount | The amount of the transaction
card | An object specifying the card that made the transaction
cardTransactionId | the id of the transaction
category | An object specifing the category for the transaction
note | Notes for the transaction
payee  | An object specifying the payee for that transaction
status | PENDING, COMPLETE or DECLINED
tags | An array of tags associated with that transaction
transactionDate | The date that transaction happened
type | CREDIT - for credit Transactions and DEBIT - for DEBIT/PIN transactions


### Card Fields

Field | Description
----- |-----
alias | the alias of the card
cardId | the id of the card


### Category Fields

Field | Description
-----| ----
transactionCategoryId | the Id of the category
description | Category description
name | The name of the category
group | What group that category belongs to
type | SPENDING or SYSTEM

### Payee Fields

Field | Description
-----|----
name  | Name of the merchant
country | The country code of the merchant
city | The city of the merchant
state | the State of the merchant
zip | The zipcode of the merchant



```json


{
      "amount": -5.5,
      "card": {
          "alias": "Farhan Ahmad",
          "cardId": 12
      },
      "cardTransactionId": 63648,
      "category": {
          "description": "Rental Cars, Airlines, Public Transit, Etc.",
          "group": "Travel & Hotels",
          "name": "Travel & Transportation",
          "transactionCategoryId": 3,
          "type": "SPENDING"
      },
      "note": "",
      "payee": {
          "city": "MILLBRAE",
          "country": "840",
          "name": "ACE PARKING 4186      ",
          "state": "CA",
          "zip": "94030"
      },
      "status": "COMPLETE",
      "tags": [],
      "transactionDate": "Nov 17, 2015 4:19:13 AM",
      "type": "CREDIT"
}

```


## Get Transactions

List all transactions for a user.

### HTTP Request 

`GET /api/transactions`



This endpoint supports query params:

### Query Params

Param | Description
---- | ----
search | The search string.
index  | The index of the first transaction to list
limit | How many transactions should return
status  | Status of the transaction: PENDING, COMPLETE, CANCELED, DECLINED
type | The type of transaction: DEBIT, CREDIT, LOAD, UNKNOWN
dateStart | The initial date to list
dateEnd | The final date to list
cards | a list of cards to show transactions
tags | a list of tags to show transactions
categories | a list of categories to show
categoryType | show only transactions for that categoryType
cardLifeCycle | show only transaction for cards with specific lifecycle


```json
{
    "amount": -42258.49,
    "cardTransactions": [
        {
            "amount": -5.5,
            "business": {
                "businessId": 6
            },
            "card": {
                "alias": "Business Owner",
                "cardId": 12
            },
            "cardTransactionId": 63648,
            "category": {
                "description": "Rental Cars, Airlines, Public Transit, Etc.",
                "group": "Travel & Hotels",
                "name": "Travel & Transportation",
                "transactionCategoryId": 3,
                "type": "SPENDING"
            },
            "note": "",
            "payee": {
                "city": "MILLBRAE",
                "country": "840",
                "name": "ACE PARKING 4186      ",
                "state": "CA",
                "zip": "94030"
            },
            "status": "COMPLETE",
            "tags": [],
            "transactionDate": "Nov 17, 2015 4:19:13 AM",
            "type": "CREDIT"
        },
        {
            "amount": -37.5,
            "business": {
                "businessId": 6
            },
            "card": {
                "alias": "Business Owner",
                "cardId": 12
            },
            "cardTransactionId": 63609,
            "category": {
                "description": "Restaurants",
                "group": "Food & Drink",
                "name": "Restaurants",
                "transactionCategoryId": 14,
                "type": "SPENDING"
            },
            "note": "",
            "payee": {
                "city": "BURBANK",
                "country": "840",
                "name": "BURBANK AIRPORT FOOD A",
                "state": "CA",
                "zip": "91505"
            },
            "status": "COMPLETE",
            "tags": [],
            "transactionDate": "Nov 17, 2015 12:31:10 AM",
            "type": "CREDIT"
        },
        {
            "amount": -286.8,
            "business": {
                "businessId": 6
            },
            "card": {
                "alias": "Employee 1",
                "cardId": 927
            },
            "cardTransactionId": 63559,
            "category": {
                "description": "Clothing, Variety, Sporting Goods, etc.",
                "group": "Retail & Goods",
                "name": "Retail and Miscellaneous Stores",
                "transactionCategoryId": 11,
                "type": "SPENDING"
            },
            "note": "",
            "payee": {
                "city": "www.AMZN/frsh",
                "country": "840",
                "name": "AmazonFresh",
                "state": "WA",
                "zip": "98102"
            },
            "status": "COMPLETE",
            "tags": [],
            "transactionDate": "Nov 16, 2015 10:29:20 PM",
            "type": "CREDIT"
        },
        {
            "amount": -25.78,
            "business": {
                "businessId": 6
            },
            "card": {
                "alias": "Employee 2",
                "cardId": 18
            },
            "cardTransactionId": 63473,
            "category": {
                "description": "Restaurants",
                "group": "Food & Drink",
                "name": "Restaurants",
                "transactionCategoryId": 14,
                "type": "SPENDING"
            },
            "note": "",
            "payee": {
                "city": "PASADENA",
                "country": "840",
                "name": "PANERA BREAD #1149",
                "state": "CA",
                "zip": "91107"
            },
            "status": "COMPLETE",
            "tags": [],
            "transactionDate": "Nov 16, 2015 7:37:20 PM",
            "type": "CREDIT"
        },
        {
            "amount": -2520.77,
            "business": {
                "businessId": 6
            },
            "card": {
                "alias": "Employee 2",
                "cardId": 18
            },
            "cardTransactionId": 62972,
            "category": {
                "description": "Insurance, Legal, Real Estate, Doctors, Medical, etc.",
                "group": "Services",
                "name": "Professional Services",
                "transactionCategoryId": 8,
                "type": "SPENDING"
            },
            "note": "",
            "payee": {
                "city": "8666724551",
                "country": "840",
                "name": "PAYPAL *MICROSOFTON   ",
                "state": "CA",
                "zip": "95131"
            },
            "status": "COMPLETE",
            "tags": [],
            "transactionDate": "Nov 16, 2015 2:54:39 AM",
            "type": "CREDIT"
        },
        {
            "amount": -1284.52,
            "business": {
                "businessId": 6
            },
            "card": {
                "alias": "Employee 3",
                "cardId": 927
            },
            "cardTransactionId": 62877,
            "category": {
                "description": "Laundries, Dry Cleaners, Barbers, Hairdressers, Shoe Repair,e tc.",
                "group": "Services",
                "name": "Personal Services",
                "transactionCategoryId": 10,
                "type": "SPENDING"
            },
            "note": "",
            "payee": {
                "city": "Oakland",
                "country": "840",
                "name": "SQ *HILSCOOKING GOS   ",
                "state": "CA",
                "zip": "94609"
            },
            "status": "COMPLETE",
            "tags": [],
            "transactionDate": "Nov 15, 2015 4:33:27 PM",
            "type": "CREDIT"
        }],
    "size": 4
}


```



<aside class="notice">When using a search string all other fields except pagination are ignored.</aside>


## Tag a transaction

Tags a transaction

### HTTP Request

`POST /transactions/<transactionId>/tags`

### Attributes

Parameter | Description
----|----
name | The tag name



Returns a transaction object with the tag.

```json

{
  "name": "MyTag"
}

```

## Remove a tag

`DELETE /transactions/<transactionId>/tags/<tagId>`

Returns the updated transaction without the tag.

## Comment on a transaction

`PUT /transactions/<transactionId>/notes`

### Attributes


Parameter | Description
----- |-----
text  | The note


```json

{
    "text": "This is a comment."
}

```


## Get Receipts

### HTTP Request

`GET /trasnactions/<transactionId>/receipts`



```json
[
  {
    "cardTrasnactionReceiptId": 12,
    "name": "Filename",
    "url": "http/fake.url/receipt12",
    "urlExpiresOn": 1447271882000
  }
]

```


## Get a Receipt

### HTTP Request

`GET /trasnactions/<transactionId>/receipts/<receiptId>`



```json

  {
    "cardTrasnactionReceiptId": 12,
    "name": "Filename",
    "url": "http/fake.url/receipt12",
    "urlExpiresOn": 1447271882000
  }

```


## Delete a Receipt

### HTTP Request

`DELETE /trasnactions/<transactionId>/receipts/<receiptId>`

The return will be a 200 OK with the updated transaction

## Upload a receipt

### HTTP Request

`POST /trasnactions/<transactionId>/receipts`

The content should be the image to uploaded encoded using either Base64 or Binary
<aside class="notice">Maximum size for receipts is 20Mb</aside>




