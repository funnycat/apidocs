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


## Delete a Card

Deletes a card

### HTTP Request 

`DELETE /api/cards/<cardId>`

You will get a 200 OK Response with the deleted card as an object.




