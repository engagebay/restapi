[![N|Solid](https://cdn5.engagebay.com/logo.svg)](https://www.engagebay.com/)

EngageBay REST API
=================
[EngageBay](https://www.engagebay.com/) is a simple, affordable all-in-one marketing and sales software built for growing businesses. Get the power of an enterprise software at a fraction of the cost.

### Overview

EngageBay API is structured around REST, HTTPS, and JSON/XML. API endpoint URLs are organized around resources below listed. It uses HTTP methods for indicating the action to take on a resource, and HTTP status codes for expressing error states. Resources are represented in JSON

API is in active development. Currently it allows you to access:

- Contacts
- Companies
- Deals
- Tracks
- Events
- Tasks
- Notes
- Forms
- Sequences
- Owners
- Custom Fields
- User Profile
- Tickets
- Tags
- Products

### Authentication
This is an HTTPS-only API. All requests to the API are authenticated by providing your REST API Key as a header value. 

The REST API key should be provided as an HTTP header named ```Authorization```.

###### API Key
You can find your API Key in the EngageBay Account Admin Settings -> API -> REST API Key.

###### End Points
All API requests should be made to: https://app.engagebay.com/

Note: All data is case-sensitive. Emails, names and other values are case sensitive. For example, "Test" and "test" are considered two different words.

### System Fields
- Contact

Following are the variable names and associations allowed in ```properties``` list of contact entity

| Variable  | Mapped to | Sub Type | Data Type |
| ------------- | ------------- | ------------- | ------------- |
| name  | First Name | - |  String | 
| last_name  | Last Name  | - | String | 
| email  | Email | primary, secondary | String | 
| role  | Role | - | String | 
| phone  | Phone Number | work, home, mobile, home_fax, work_fax, other | String | 
| website  | Website | url, skype, twitter, linkedin, facebook, xing, feed, google-plus, flickr, github, youtube | String | 
| address  | Address | - | JSON String (Ex: {"address": "EngageBay Inc, 255 Verano Way", "city":"Mountain House", "state":"CA", "country": "USA", "zip": "95391"}) | 


Following are the variable names and associations allowed in contact entity

| Variable  | Mapped to | Sub Type | Data Type |
| ------------- | ------------- | ------------- | ------------- |
| tags  | Tags | - |  Array Ex: [{tag: "Tag1"}] | 
| score  | Score  | - | Number | 
| owner_id  | Owner of the Contact | - | Number (User Id) | 


- Company

Following are the variable names and associations allowed in ```properties``` list of company entity

| Variable  | Mapped to | Sub Type | Data Type |
| ------------- | ------------- | ------------- | ------------- |
| name  | Company Name | - |  String | 
| url  | Company Domain (URL)  | - | String | 
| email  | Company Email | - | String | 
| phone  | Phone Number | work, home, mobile, home_fax, work_fax, other | String | 
| website  | Website | url, skype, twitter, linkedin, facebook, xing, feed, google-plus, flickr, github, youtube | String | 
| address  | Address | - | JSON String (Ex: {"address": "EngageBay Inc, 255 Verano Way", "city":"Mountain House", "state":"CA", "country": "USA", "zip": "95391"}) | 


Following are the variable names and associations allowed in company entity

| Variable  | Mapped to | Sub Type | Data Type |
| ------------- | ------------- | ------------- | ------------- |
| tags  | Tags | - |  Array Ex: [{tag: "Tag1"}] | 
| score  | Score  | - | Number | 
| owner_id  | Owner of the Contact | - | Number (User Id) | 


- Deal

Following are the variable names and associations allowed in deal entity

| Variable  | Mapped to | Data Type |
| ------------- | ------------- | ------------- |
| name  | Deal Name | String |
| unique_id  | Deal ID |  Number |
| description  | Description | String |
| track_id  | Deal Track |  Number |
| amount  | Amount | Number |
| currency_type  | Currency Name | Currency Code (Ex: USD-$) |
| closed_date  | Close Date | Date (Should be in user selected format) |
| tags  | Tags |  Array Ex: [{tag: "Tag1"}] |
| owner_id  | Owner of the Contact | Number (User Id) | 

- Ticket

Following are the variable names and associations allowed in ticket entity

| Variable  | Mapped to | Data Type |
| ------------- | ------------- | ------------- |
| subject  | Ticket Subject | String |
| type  | Ticket Type |  Number |
| priority  | Ticket Priority | Number |
| status  | Ticket Status |  Number |
| group_id  | Group ID | Number |
| assignee_id  | User ID | Number |
| html_body  | Ticket Body Message | String |
| tags  | Tags |  Array Ex: [{tag: "Tag1"}] |


### Custom Fields
While requesting an API call, all custom fields should have field_type property. You can find/create custom fields in your EngageBay account Admin Settings -> Custom Fields ->Contact/Deal/Company. 

Supporting field_types are TEXT, DATE, LIST, CHECKBOX, TEXTAREA, NUMBER, FORMULA, MULTICHECKBOX, URL, CURRENCY, PHONE, FILE.

Note: Custom fields will have subtypes. Only the above mentioned subtype for those respective properties should be specified by the user.

| Field Type  | Data Type | 
| ------------- | ------------- | 
| TEXT  | String | 
| DATE  | DATE (DD/MM/YYYY - Should be user selected format) |  
| LIST  | String |
| CHECKBOX  | Boolean |
| TEXTAREA  | String |
| NUMBER  | Number |
| CURRENCY  | Mathematical Expression witn field names |
| MULTICHECKBOX  | String |
| URL  | String |
| PHONE  | String |
| FILE  | String array |

Below is an example properties JSON with all custom field types:
```
"properties": [{
		"name": "Number Field",
		"value": "1",
		"field_type": "NUMBER",
		"type": "CUSTOM"
	}, {
		"name": "Dropdown Field",
		"value": "option_value",
		"field_type": "LIST",
		"type": "CUSTOM"
	}, {
		"name": "Text Field",
		"value": "Text Value",
		"field_type": "TEXT",
		"type": "CUSTOM"
	}, {
		"name": "DATE",
		"value": "22/07/2020",
		"field_type": "DATE",
		"type": "CUSTOM"
	}, {
		"name": "Checkbox Field",
		"value": "true",
		"field_type": "CHECKBOX",
		"type": "CUSTOM"
	}, {
		"name": "Textarea Field",
		"value": "Textarea Content Places Here",
		"field_type": "TEXTAREA",
		"type": "CUSTOM"
	}, {
		"name": "Phone Number Field",
		"value": "(040)-2963213",
		"field_type": "PHONE",
		"type": "CUSTOM"
	}, {
		"name": "Website Field",
		"value": "https://developers.google.com",
		"field_type": "URL",
		"type": "CUSTOM"
	}, {
		"name": "Multiple Checkbox Field",
		"value": "box1,box2",
		"field_type": "MULTICHECKBOX",
		"type": "CUSTOM"
	}, {
		"name": "Files",
		"value": "[\"https://drive.google.com/files/test.csv\",\"https://drive.google.com/files/test2.csv\"]",
		"field_type": "FILE",
		"type": "CUSTOM"
	}]
```

### Date Format
Values for DATE should be like the date format selected by API key user. You can find the date format here - Preferences -> Dateformat Ex: DD/MM/YYYY -> 31/07/2019 12:00:00 Date will be saved in the timezone selected by user.

### Errors
HTTP status codes are used by the API to indicate that an error has occurred while processing a request. There are four main error status codes used by the API:

| Code  | Description |
| ------------- | ------------- |
| 400  | The request could not be processed, usually due to a missing or invalid parameter. |
| 401  | The request could not be authenticated or the authenticated user is not authorized to access the requested endpoint.  |
| 404  | The requested endpoint does not exist.  |
| 429  | The user has sent too many requests in a given amount of time ("limit rate") - contact EngageBay support for more details.  |

Here is an example: 
401 Unauthorized
```
{
  "error": "UnAuthenticated User",
  "status": "401"
}
```
400 Bad Request
```
{
"error": "Invalid input. Please provide all the required fields."
}
```

### Getting Started

**[Contacts](#1-contacts---companies-api)**
* [1 Listing contacts](#11-listing-contacts)
* [2 Get contact by ID](#12-get-contact-by-id)
* [3 Creating a contact](#13-creating-a-contact)
* [4 Updating a contact](#14-update-properties-of-a-contact-by-id-partial-update)
* [5 Delete single contact](#15-delete-single-contact)
* [6 Get contact based on email address](#115-get-contact-based-on-email-address)
* [7 Adding tags to a contact based on email address](#16-adding-tags-to-a-contact-based-on-email-address)
* [8 Delete tags to a contact based on email address](#17-delete-tags-to-a-contact-based-on-email-address)
* [9 List tags for a contact based on email address](#18-list-tags-for-a-contact-based-on-email-address)
* [10 Add score to a contact using email address](#19-add-score-to-a-contact-using-email-address)
* [11 Search contacts](#110-search-contacts)
* [12 List tags for a contact by ID](#111-list-tags-for-a-contact-by-id)
* [13 Adding tags to a contact by ID](#112-adding-tags-to-a-contact-by-id)
* [14 Delete tags value by ID](#113-delete-tags-value-by-id)
* [15 Change contact owner](#114-change-contact-owner)
* [16 Creating a batch of contacts](#116-creating-a-batch-of-contacts)
* [17 Get contact notes](#117-get-contact-notes)
* [18 Get contact call logs](#118-get-contact-call-logs)

**[Company APIs](#21-creating-a-company)**

* [1 Creating a company](#21-creating-a-company)
* [2 Updating a company](#22-update-properties-of-a-company-by-id-partial-update)
* [3 Get list of companies](#23-get-list-of-companies)
* [4 Get company by id](#24-get-company-by-id)
* [5 Delete single company](#25-delete-single-company)
* [6 Search companies](#26-search-companies)
* [7 Add contact to company by contact Id](#27-add-contact-to-company-by-contact-Id)
* [8 Add contact to company using email address](#28-add-contact-to-company-using-email-address)

**[Deals](#31-listing-deals)**

* [1 Listing deals](#31-listing-deals)
* [2 Get deal by its ID](#32-get-deal-by-its-id)
* [3 Create a deal](#33-create-a-deal)
* [4 Delete a deal](#34-delete-a-deal)
* [5 Create deal to a contact using email address](#35-create-deal-to-a-contact-using-email-address)
* [6 Search deals](#36-search-deals)
* [7 Update deal track](#37-update-deal-track)
* [8 Updating a deal](#38-update-properties-of-a-deal-by-id-partial-update)

**[Tracks](#41-get-list-of-tracks)**

* [1 Get all tracks](#41-get-all-tracks)
* [3 Create track](#42-create-track)
* [4 Update track](#43-update-track)
* [5 Get track by ID](#44-get-track-by-id)
* [6 Delete track by ID](#45-delete-track-by-id)


**[Events](#51-get-list-of-events)**

* [1 Get list of events](#51-get-list-of-events)
* [2 Get events related to contact](#52-get-events-related-to-contact)
* [3 Create event](#53-create-event)
* [4 Update event](#54-update-event)


**[Tasks](#61-listing-tasks)**

* [1 Get the list of tasks based on given filters](#61-get-the-list-of-tasks-based-on-given-filters)
* [2 Get the task based on ID](#62-get-the-task-based-on-id)
* [3 Create task](#63-create-task)
* [4 Update task](#64-update-task)
* [5 Delete a task based on ID](#65-delete-a-task-based-on-id)


**[Notes](#71-create-a-note)**
* [1 Create a note](#71-create-a-note)


**[Forms](#81-listing-forms)**

* [1 List of forms](#81-list-of-forms)
* [2 Add contact to a form](#82-add-contact-to-a-form)



**[Sequences](#91-add-contact-to-a-sequence)**

* [1 Add contact to a sequence](#91-add-contact-to-a-sequence)



**[Lists](#101-list-of-lists-)**

* [1 List of lists](#101-list-of-lists)
* [2 Add contact to list](#102-add-contact-to-list)



**[Owners](#111-get-list-of-owners)**

* [1 Get list of owners](#111-get-list-of-owners)


**[CustomFields](#121-get-list-of-custom-fields)**

* [1 Get list of custom fields](#121-get-list-of-custom-fields)
* [2 Create a custom field](#122-create-a-custom-field)
* [3 Delete a custom field](#123-delete-a-custom-field-)

**[User Profile](#131-get-user-profile-)**
* [1 Get user profile](#131-get-user-profile-)

**[Tickets](#141-get-list-of-tickets)**

* [1 Listing tickets](#141-get-list-of-tickets)
* [2 Listing tickets by filter](#142-get-list-of-tickets-by-filter)
* [3 Get ticket by ID](#145-get-ticket-by-id)
* [3 Create a ticket](#143-create-a-ticket)
* [4 Delete a ticket](#144-delete-a-ticket)

**[Tags](#151-list-of-tags)**

* [1 List of Tags](#151-list-of-tags)
* [2 Add Tag](#152-add-tag)

**[Products](#161-list-of-products)**

* [1 List of products](#161-list-of-products)
* [2 Get product by ID](#162-get-product-by-id)
* [3 Creating a product](#163-creating-a-product)
* [4 Updating a product](#164-update-a-product-by-id)
* [5 Updating a product](#165-update-properties-of-a-product-by-id-partial-update)
* [6 Get product by Name](#166-get-product-by-name)
* [7 Delete single product](#167-delete-single-product)
* [8 Add a product to contact](#168-add-a-product-to-contact)
* [9 Delete a product from contact](#169-delete-a-product-from-contact)

**[Broadcast](#171-creating-a-broadcast)**
* [1 Create a Broadcast](#171-creating-a-broadcast)

### 1.1 Listing contacts: 
- Returns a list of your contacts

For the Response in JSON format, add the header 'Accept' as application/json. By default, the response will be in XML format. Paging can be applied using the page_size and cursor query parameters. Cursor for the next page will be in the last contact of the list. If there is no cursor, it means that it is the end of list.

###### Endpoint
POST dev/api/panel/subscribers

###### Optional parameters
- ``page_size `` - Page size for paginated results.
- ``sort_key`` - Sort order for results. Set it to created_time/updated_time to sort list in ascending order. 		Prepened - to sort in descending.
- ``cursor`` - To get next set of resultset. You will get it in the last record of previous resultset.

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json"  \
-d "page_size=10&sort_key=-created_time" \
"https://app.engagebay.com/dev/api/panel/subscribers"
```

###### Example JSON response
```javascript
[
  {
	"id": 4997280348241920,
	"owner_id": 6192449487634432,
	"name": "Test Contact",
	"email": "testcontact@gmail.com",
	"score": 5
	"created_time": 1535538585,
	"updated_time": 0,
	"status": "CONFIRMED",
	"companyIds": [5278755324952576],
	"properties": [{
		"name": "name",
		"value": "Test Contact",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "last_name",
		"value": "1",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "testcontact@gmail.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "phone",
		"value": "+91 9999999999",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"listIds": [],
	"tags": [{
		"tag": "United States",
		"assigned_time": 1535538585
	}],
	"emailBounceStatus": []
},{
	"id": 4997280348241920,
	"owner_id": 6192449487634432,
	"name": "Test Contact 2",
	"email": "testcontact2@gmail.com",
	"score": 5
	"created_time": 1535538585,
	"updated_time": 0,
	"status": "CONFIRMED",
	"companyIds": [5278755324952576],
	"properties": [{
		"name": "name",
		"value": "Test Contact 2",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "last_name",
		"value": "1",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "testcontact2@gmail.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "phone",
		"value": "+91 9999999999",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"listIds": [],
	"tags": [{
		"tag": "United States",
		"assigned_time": 1535538585
	}],
	"emailBounceStatus": [],
	"cursor": "Cl0KFgoMY3JlYXRlZF90aW1lEgYI2IWV3AUSP2oRYWNjb3VudGJveC0xNTQ2MDVyFwsSClN1YnNjcmliZXIYgICAgIDAowgMogEQNTYyOTQ5OTUzNDIxMzEyMBgAIAE",
}
]
```
### 1.2 Get contact by ID
Returns data for a single contact
###### Endpoint
GET /dev/api/panel/subscribers/{id}
###### Required parameters
``id`` - Contact Id.
###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
"https://app.engagebay.com/dev/api/panel/subscribers/1"
```
###### Example JSON response
```javascript
[{
	"id": 4997280348241920,
	"owner_id": 6192449487634432,
	"name": "Test Contact",
	"firstname": "Test Contact",
	"lastname": "1",
	"fullname": "Test Contact 1",
	"name_sort": "test contact",
	"email": "testcontact@gmail.com",
	"created_time": 1535538585,
	"updated_time": 0,
	"status": "CONFIRMED",
	"sources": [{
		"type": "DEFAULT",
		"subscribed_on": 1535538585,
		"status": "ACTIVE",
		"custom": 0
	}],
	"companyIds": [5278755324952576],
	"contactIds": [],
	"properties": [{
		"name": "name",
		"value": "Test Contact",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "last_name",
		"value": "1",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "testcontact@gmail.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "phone",
		"value": "+91 9999999999",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "country",
		"value": "United States",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"listIds": [],
	"owner": {
		"id": 6192449487634432,
		"email": "test@test.com",
		"name": "test"
	},
	"entiy_group_name": "subscriber",
	"tags": [{
		"tag": "United States",
		"assigned_time": 1535538585
	}],
	"broadcastIds": [],
	"openedLinks": [],
	"emailProperties": [],
	"unsubscribeList": [],
	"emailBounceStatus": [],
	"importedEntity": false,
	"forceCreate": false,
	"forceUpdate": false,
	"score": 5
}]
```
### 1.3 Creating a contact:  

Accepts contact JSON as post data along with the credentials of domain User (User name and API Key).
- Each field is case sensitive.
- Please don't pass null value.
- If you don't know value of field then either don't pass that field or pass empty data to a field.

###### Endpoint
POST dev/api/panel/subscribers/subscriber

###### Acceptable request representation:
```
{
	"score" : 10,
	"properties": [{
		"name": "name",
		"type": "SYSTEM"
	},{
		"name": "email",
		"value": "samplecontact@engagebay.com",
		"type": "SYSTEM"
	}, {
		"name": "phone",
		"value": "+91 9999999999",
		"type": "SYSTEM"
	}, {
		"name": "custom",
		"value": "cutom",
		"type": "CUSTOM",
		"field_type": "TEXT",
		"is_searchable": true
	}, {
		"name": "custom field name 2",
		"value": "11/14/1988 03:31:11",
		"type": "CUSTOM",
		"field_type": "DATE",
		"is_searchable": true
	}],
	"tags" : ["sample", "sample1"]
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
	"score" : 10,
	"properties": [{
		"name": "name",
		"value": "sample",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	},{
		"name": "email",
		"value": "samplecontact@engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "phone",
		"value": "+91 9999999999",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "custom",
		"value": "cutom",
		"field_type": "TEXT",
		"is_searchable": true,
		"type": "CUSTOM"
	}],
	"tags" : [{"tag": "sample"}]
}' \
"https://app.engagebay.com/dev/api/panel/subscribers/subscriber"
```
### 1.4 Update properties of a contact by ID (partial update): 
- Updates the properties for a single contact.

We can update the required property fields of the contact using this call. It is used to add a new property or update the existing property. It accepts property object of the contact with a valid parameter in it. Send the ContactId of the contact to identify it. This will not affect other fields.

Using this API you can not delete properties.If subtype is same for phone,website or email then value can be overridden. Lead score, star value and tags can not be updated using this API.

###### Endpoint
PUT dev/api/panel/subscribers/update-partial

###### Optional parameters
- ``properties`` - Updated custom fields for your contact as object of key/value pairs.

###### Acceptable request representation
```sh
curl -i -X PUT  \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "id": 6218728647688192,
    "properties": [{
		"name": "name",
		"value": "test",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "last_name",
		"value": "testlast",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "sarah@engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}]
}' \
"https://app.engagebay.com/dev/api/panel/subscribers/update-partial"
```
### 1.5 Delete single contact: 
- Delete the single contact from account
###### Endpoint
DELETE dev/api/panel/subscribers/{contact-id}

###### Example Request
```sh
curl -i -X DELETE \
"https://app.engagebay.com/dev/api/panel/subscribers/{contact-id}"
```
### 1.15 Get contact based on email address: 
Returns data for a single contact by contact email
###### Endpoint
GET /dev/api/panel/subscribers/contact-by-email/{email}
###### Required parameters
``email`` - Email address of the contact.
###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
"https://app.engagebay.com/dev/api/panel/subscribers/contact-by-email/{email}"
```
###### Example JSON response
```javascript
[{
	"id": 4997280348241920,
	"owner_id": 6192449487634432,
	"name": "Test Contact",
	"firstname": "Test Contact",
	"lastname": "1",
	"fullname": "Test Contact 1",
	"name_sort": "test contact",
	"email": "testcontact@gmail.com",
	"created_time": 1535538585,
	"updated_time": 0,
	"status": "CONFIRMED",
	"sources": [{
		"type": "DEFAULT",
		"subscribed_on": 1535538585,
		"status": "ACTIVE",
		"custom": 0
	}],
	"companyIds": [5278755324952576],
	"contactIds": [],
	"properties": [{
		"name": "name",
		"value": "Test Contact",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "last_name",
		"value": "1",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "testcontact@gmail.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "phone",
		"value": "+91 9999999999",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "country",
		"value": "United States",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"listIds": [],
	"owner": {
		"id": 6192449487634432,
		"email": "test@test.com",
		"name": "test"
	},
	"entiy_group_name": "subscriber",
	"tags": [{
		"tag": "United States",
		"assigned_time": 1535538585
	}],
	"broadcastIds": [],
	"openedLinks": [],
	"emailProperties": [],
	"unsubscribeList": [],
	"emailBounceStatus": [],
	"importedEntity": false,
	"forceCreate": false,
	"forceUpdate": false,
	"score": 5
}]
```

### 1.6 Adding tags to a contact based on email address: 
Searches for the contact based on the given email address and adds the given tags to the contact. You can add multiple tags. Tags should be sent as an array. Email address (email) and tags (tags) array should be sent as a form parameter (Content-Type: application/x-www-form-urlencoded).Tag name should start with an alphabet and cannot contain special characters other than underscore and space.
###### Endpoint
POST dev/api/panel/subscribers/email/tags/add
###### Required parameters
``Email`` - Email address of the contact
``tags`` -  Tags to be added to the contact

###### Example request
```sh
curl -i -X POST \
-H "Accept: application/json" \
-H "Authorization: xxxxxxxxx" \
-H "Content-Type:application/x-www-form-urlencoded" \
-d 'email=samson@engagebay.com&tags=["testsample"]' \
"https://app.engagebay.com/dev/api/panel/subscribers/email/tags/add"
```
### 1.7 Delete tags to a contact based on email address: 
Searches for the contact based on the given email address and searches for the given tag in the contact's tag list. If there is a match, then it deletes that tag. You can delete multiple tags. Tags should be sent as an array. Email address (email) and tags (tags) array should be sent as a form parameter(Content-Type: application/x-www-form-urlencoded)
###### Endpoint
POST dev/api/panel/subscribers/email/tags/delete
###### Required parameters
``Email`` - Email address of the contact
``tags`` -  Tags to be deleted for the contact

###### Example request
```sh
curl -i -X POST \
-H "Accept: application/json"
-H "Authorization: xxxxxxxxx" \
-H "Content-Type:application/x-www-form-urlencoded" \
-d 'email=sample@engagebay.com&tags=["sampletest"]' \
"https://app.engagebay.com/dev/api/contacts/email/tags/delete "
```

### 1.8 List tags for a contact based on email address: 
Lists all the tags for a contact
###### Endpoint
POST dev/api/panel/subscribers/get-tags/{subscriber-email}
###### Required parameters
``Email`` - Email address of the contact

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type:application/x-www-form-urlencoded" \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/subscribers/get-tags/{subscriber-email}"
```
###### Example JSON response
```
[{
	"tag": "sampletag1",
	"assigned_time": 1535709035
},{
	"tag": "sampletag2",
	"assigned_time": 1535709035
}]
```

### 1.9 Add score to a contact using email address: 
Add or change the score of the contact using the contact's email address.
###### Endpoint
POST dev/api/panel/subscribers/add-score
###### Required parameters
``Email`` - Email address of the contact
``score`` - Score value

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type:application/x-www-form-urlencoded" \
-d 'email=samson@walt.ltd&score=100' \
"https://app.engagebay.com/dev/api/panel/subscribers/add-score"
```

### 1.10 Search contacts:

- Search using keyword.

###### Required parameters
``q`` - Search keyword (all contact default fields will be searched).
``page_size`` - Number of results to fetch
``type`` - Should be 'Subscriber' for searching Contacts

###### Endpoint
GET dev/api/search?q=searchtext&type=Subscriber

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxx" \
 "https://app.engagebay.com/dev/api/search?q=test&type=Subscriber"
```
###### Example JSON response
```javascript
[{
	"count": 1,
	"id": 5604787936559104,
	"owner_id": 5676618345349120,
	"name": "test",
	"firstname": "test",
	"lastname": "",
	"fullname": "test ",
	"name_sort": "test",
	"email": "test@engagebay.com",
	"created_time": 1540474374,
	"updated_time": 1540962133,
	"status": "CONFIRMED",
	"sources": [{
		"type": "DEFAULT",
		"subscribed_on": 1540474374,
		"status": "ACTIVE",
		"custom": 0
	}],
	"companyIds": [],
	"contactIds": [],
	"properties": [{
		"name": "name",
		"value": "test",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "test@engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"listIds": [],
	"entiy_group_name": "subscriber",
	"tags": [{
		"tag": "import",
		"assigned_time": 1540474374
	}],
	"score": 20
}]
```

### 1.11 List tags for a contact by ID: 
Lists all the tags for a contact by contact ID
###### Endpoint
GET dev/api/panel/subscribers/get-tags-by-id/{contactId}
###### Required parameters
``contactId`` - ID of the contact

###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type:application/x-www-form-urlencoded" \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/subscribers/get-tags-by-id/{contactId}"
```
###### Example JSON response
```
[{
	"tag": "sampletag1",
	"assigned_time": 1535709035
},{
	"tag": "sampletag2",
	"assigned_time": 1535709035
}]
```

### 1.12 Adding tags to a contact by ID: 
Searches for the contact based on the given contact ID and adds the given tags to the contact. You can add multiple tags. Tags should be sent as an array. tags (tags) array should be sent as a form parameter (Content-Type: application/x-www-form-urlencoded).Tag name should start with an alphabet and cannot contain special characters other than underscore and space.
###### Endpoint
POST dev/api/panel/subscribers/contact/tags/add2/{contactId}
###### Required parameters
``contactId`` - ID of the contact
``tags`` -  Tags to be added to the contact

###### Example request
```sh
curl -i -X POST \
     -H "Accept:application/json" \
     -H "Authorization:xxxxxxxxxx" \
     -H "Content-Type:application/json" \
     -d '[
	   {"tag" : "sample1"},
	   {"tag" : "sample2"} 
	   ]' \
"https://app.engagebay.com/dev/api/panel/subscribers/contact/tags/add2/{contactId}"
```

### 1.13 Delete tags value by ID:

- Delete tag values by contact id.

###### Required parameters

``contactId`` - ID of the contact.
``tags`` - List of tags to delete

###### Endpoint

POST dev/api/panel/subscribers/contact/tags/delete/{contactId}

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d '[
   	{"tag" : "sample1"},
   	{"tag" : "sample2"} 
   	]' \
 "https://app.engagebay.com/dev/api/panel/subscribers/contact/tags/delete/{contactId}"
```

### 1.14 Change contact owner:

- Change contact owner using owner email and contact Id.

###### Required parameters

``subscriberId`` - ID of the contact.
``ownerEmail`` - Owner Email

###### Endpoint

POST dev/api/panel/subscribers/update-owner-by-email?subscriberId=5015780936646656&ownerEmail=test@engagebay.com

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:p5nlcfg7m89a8lb9gf1p1nf6bd" \
   -H "Content-Type:application/json" \
 "https://app.engagebay.com/dev/api/panel/subscribers/update-owner-by-email?subscriberId=5015780936646656&ownerEmail=test@engagebay.com"
```
#### 
```javascript
{
	"id": 5015780936646656,
	"owner_id": 5676618345349120,
	"name": "homer8",
	"firstname": "homer8",
	"lastname": "",
	"fullname": "homer8 ",
	"name_sort": "homer8",
	"email": "homer@snpp8.com",
	"created_time": 1542786798,
	"updated_time": 1542793315,
	"status": "CONFIRMED",
	"sources": [{
		"type": "DEFAULT",
		"id": 0,
		"subscribed_on": 1542786798,
		"status": "ACTIVE",
		"custom": 0
	}],
	"companyIds": [],
	"contactIds": [],
	"properties": [{
		"name": "name",
		"value": "homer8",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	},{
		"name": "email",
		"value": "homer@snpp8.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"listIds": [4893748567736320],
	"entiy_group_name": "subscriber",
	"tags": [{
		"tag": "Zapier tag",
		"assigned_time": 1542788077
	}, {
		"tag": "Zapier",
		"assigned_time": 1542788077
	}],
	"score": 20
}
```
### 1.16 Creating a batch of contacts:  
This endpoint is used to create a group of contacts. Performance is optimal when the batch size is limited to 100 contacts or fewer. It accepts JSON with an array of contacts and a callback URL to notify you after completion. The Callback URL field is optional here.

Note: Please note that changes made through this endpoint are processed asynchronously, so it may take several minutes for the changes to be applied to contact records. The callback URL is used to track the completion of contact synchronization, including successful and failed records.


Ensure that the batch size does not exceed 100 contacts per request. Multiple batch requests are not supported, and attempting to do so will result in an error if a batch request is already running.

When using this endpoint, please keep in mind the following:
- Each field is case sensitive.
- Do not pass null values.
- If you don't have a value for a field, either omit the field or provide empty data.

###### Endpoint
POST dev/api/panel/subscribers/subscriber-batch

###### Example request
```sh
curl -i -X POST \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
  "callbackURL": "https://domainname.com/notify-me",
  "contacts": [
    {
      "score": 1,
      "properties": [
        {
          "name": "name",
          "value": "name1"
        },
        {
          "name": "email",
          "value": "name1@domain.com"
        }
      ],
      "tags": [
        "sample",
        "sample1"
      ]
    },
    {
     "score": 2,
      "properties": [
        {
          "name": "name",
          "value": "name2"
        },
        {
          "name": "email",
          "value": "name2@domain.com"
        }
      ],
      "tags": [
        "sample",
        "sample1"
      ]
    }
  ]
}' \
"https://app.engagebay.com/dev/api/panel/subscribers/subscriber-batch"
```
###### Example JSON response
```
{"status":"success"}
```

### 1.17 Get contact notes: 
This endpoint is used to retrieve notes of contact by contactID. Page_size, sort_key and cursor should be sent as a query parameter. Paging can be applied using the page_size and cursor form parameters. Cursor for the next page will be in the last note of the list. If there is no cursor, it means that it is the end of the list.

###### Endpoint
GET dev/api/panel/notes/<contactID>

###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/notes/<contactID>"
```

###### Example JSON response
```
[
    {
        "id": 5696837256740864,
        "parentId": 5106855652098048,
        "subject": "Test note subject2",
        "content": "<!DOCTYPE html>\n<html>\n<head>\n</head>\n<body>\n<div>Test note content2</div>\n</body>\n</html>",
        "force": false,
        "syncIds": [],
        "owner_id": 5769015641243648,
        "type": "PUBLIC",
        "created_time": 1652857810,
        "updated_time": 1652857810,
        "source": "SUBSCRIBER",
        "createFollowUpTask": false
    },
    {
        "id": 5958896380805120,
        "parentId": 5106855652098048,
        "subject": "Test note subject",
        "content": "<!DOCTYPE html>\n<html>\n<head>\n</head>\n<body>\n<div>Test note content</div>\n</body>\n</html>",
        "force": false,
        "syncIds": [],
        "owner_id": 5769015641243648,
        "type": "PUBLIC",
        "created_time": 1652857798,
        "updated_time": 1652857798,
        "source": "SUBSCRIBER",
        "createFollowUpTask": false
    }
]
```

### 1.18 Get contact call logs: 
This endpoint is used to retrieve call logs of contact by contactID. Contact_id, page_size, sort_key and cursor should be sent as a query parameter. Paging can be applied using the page_size and cursor form parameters. Cursor for the next page will be in the last call log of the list. If there is no cursor, it means that it is the end of the list.

###### Endpoint
GET dev/api/panel/call-logs?contact_id={contactID}

###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/call-logs?contact_id=<contactID>"
```

###### Example JSON response
```
[
    {
        "id": 5016633388040192,
        "created_time": 1613497668,
        "contact_id": 5106855652098048,
        "call_id": "CAb740cf69cef35dc2ef9838024e939251",
        "duration": 0,
        "status": "NOT_ANSWERED",
        "status_legacy": "no-answer",
        "to_number": "+441743562350",
        "from_number": "+447593532685",
        "account_id": "AC532b020f926f9a512989da92105ff462",
        "caller_type": "twilio",
        "started_at": 1613497666,
        "recording_url": "https://api.twilio.com/2010-04-01/Accounts/AC532b020f926f9a512989da92105ff462/Recordings/RE75bfd472d35dbafac8c98a8447c4fed0",
        "isManualEntry": false,
        "owner_id": 5675802922319872,
        "notes": [],
        "note": {
            "force": false,
            "syncIds": [],
            "type": "PUBLIC",
            "createFollowUpTask": false
        },
        "addNote": false,
        "forceUpdate": false,
        "sendNotificationsTo": [],
        "isVoicemail": false,
        "callType": "INBOUND",
        "reflectStatus": false,
        "call_cost": 0,
        "inActive": false
    },
    {
        "id": 5962822467977216,
        "created_time": 1613497645,
        "contact_id": 5106855652098048,
        "call_id": "CAd335cc0e31d708572d3c9e5b0a1d152e",
        "duration": 0,
        "status": "NOT_ANSWERED",
        "status_legacy": "no-answer",
        "to_number": "+441743562350",
        "from_number": "+447593532685",
        "account_id": "AC532b020f926f9a512989da92105ff462",
        "caller_type": "twilio",
        "started_at": 1613497642,
        "recording_url": "https://api.twilio.com/2010-04-01/Accounts/AC532b020f926f9a512989da92105ff462/Recordings/RE7f36bd88fd1b096750f41aa3de71bcbf",
        "isManualEntry": false,
        "owner_id": 5675802922319872,
        "notes": [],
        "note": {
            "force": false,
            "syncIds": [],
            "type": "PUBLIC",
            "createFollowUpTask": false
        },
        "addNote": false,
        "forceUpdate": false,
        "sendNotificationsTo": [],
        "isVoicemail": false,
        "callType": "INBOUND",
        "reflectStatus": false,
        "call_cost": 0,
        "inActive": false
    }
]
```


### 2.1 Creating a company: 
- Accepts company JSON as post data along with the credentials of domain User (User name and API Key).
- Each field is case sensitive.
- Please don't pass null value.
- If you don't know the value of field then don't pass that field at all or pass empty data for the field.
###### Endpoint
POST dev/api/panel/companies/company
######  Acceptable request representation:
```javascript
{
	"name": "www.engagebay.com",
	"name_sort": "www.engagebay.com",
	"url": "www.engagebay.com",
	"created_time": 1535620529,
	"updated_time": 0,
	"properties": [{
		"name": "url",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "name",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"tags": [],
	"contactIds": [],
	"entiy_group_name": "company",
	"companyIds": []
}
```
###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
	"name": "www.engagebay.com",
	"name_sort": "www.engagebay.com",
	"url": "www.engagebay.com",
	"created_time": 1535620529,
	"updated_time": 0,
	"properties": [{
		"name": "url",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "name",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"tags": [],
	"contactIds": [],
	"entiy_group_name": "company",
	"companyIds": []
} ' \
"https://app.engagebay.com/dev/api/panel/companies/company"
```

### 2.2 Update properties of a company by ID (partial update): 
- Updates the properties for a single company.

We can update required property fields of the company using this call. It is used to add a new property or update the existing property. It accepts property object of company with valid parameter in it. Send the Company-Id of the company to identify it. This will not affect other fields.

Using this API you can not delete properties.If subtype is same for phone or email then value can be overridden.

###### Endpoint
PUT dev/api/panel/companies/update-partial

###### Optional parameters
- ``properties`` - Updated custom fields for your company as object of key/value pairs.

###### Example request
```sh
curl -i -X PUT \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
	"id": 5141586283331584,
	"properties": [{
		"name": "name",
		"value": "EngageBay",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "url",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"tags": []
} ' \
"https://app.engagebay.com/dev/api/panel/companies/update-partial"
```
### 2.3 Get list of companies: 
- Get list of companies

Fetches the list of companies. Page_size, sort_key and cursor should be sent as a form parameter (Content-Type: application/x-www-form-urlencoded). Paging can be applied using the page_size and cursor form parameters. Cursor for the next page will be in the last company of the list. If there is no cursor, it means that it is the end of the list.

###### Endpoint
POST dev/api/panel/companies

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/companies"
```

###### Example JSON response
```
[{
	"id": 5670864666230784,
	"name": "www.github.com",
	"name_sort": "www.github.com",
	"url": "www.github.com",
	"created_time": 1535622004,
	"updated_time": 0,
	"properties": [{
		"name": "url",
		"value": "www.github.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "name",
		"value": "www.github.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"tags": [],
	"contactIds": [],
	"entiy_group_name": "company",
	"owner_id": 5636470266134528,
	"owner": {
		"id": 5636470266134528,
		"email": "sarah@engagehub.io",
		"name": "sarah"
	},
	"importedEntity": false,
	"forceCreate": false,
	"companyIds": []
}, {
	"id": 5141586283331584,
	"name": "www.engagebay.com",
	"name_sort": "www.engagebay.com",
	"url": "www.engagebay.com",
	"created_time": 1535620529,
	"updated_time": 0,
	"properties": [{
		"name": "url",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "name",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"tags": [],
	"contactIds": [],
	"entiy_group_name": "company",
	"owner_id": 5636470266134528,
	"owner": {
		"id": 5636470266134528,
		"email": "sarah@engagehub.io",
		"name": "sarah"
	},
	"importedEntity": false,
	"forceCreate": false,
	"companyIds": []
}]
```
### 2.4 Get company by ID: 
- Returns company object which is associated with given company id

###### Endpoint
GET dev/api/panel/companies/{id}

###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept :application/json" 
"https://app.engagebay.com/dev/api/panel/companies/{id}"
```

###### Example JSON response
```
{
	"id": 5141586283331584,
	"name": "www.engagebay.com",
	"name_sort": "www.engagebay.com",
	"url": "www.engagebay.com",
	"created_time": 1535620529,
	"updated_time": 1535622374,
	"properties": [{
		"name": "url",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "name",
		"value": "www.engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"tags": [],
	"contactIds": [],
	"entiy_group_name": "company",
	"owner_id": 5636470266134528,
	"owner": {
		"id": 5636470266134528,
		"email": "sarah@engagehub.io",
		"name": "sarah"
	},
	"importedEntity": false,
	"forceCreate": false,
	"companyIds": []
}
```

### 2.5 Delete single company: 
- Deletes company based on the id of the company, which is sent in the request URL path.

###### Endpoint
DELETE dev/api/panel/companies/{id}

###### Example request
```sh
curl -i -X DELETE  \
-H "Authorization: xxxxxxxxx" \
"https://app.engagebay.com/dev/api/panel/companies/{id}"
```

### 2.6 Search companies:

- Search using keyword.

###### Required parameters
``q`` - Search keyword (all company default fields will be searched).
``page_size`` - Number of results to fetch
``type`` - Should be 'Company' for searching companies

###### Endpoint
GET dev/api/search?q=searchtext&type=Company

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxx" \
 "https://app.engagebay.com/dev/api/search?q=samplecompany&type=Company"
```
###### Example JSON response
```javascript
[{
	"count": 1,
	"id": 5737773445152768,
	"name": "samplecompany.in",
	"name_sort": "samplecompany.in",
	"url": "samplecompany.in",
	"created_time": 1536909642,
	"updated_time": 1542103938,
	"properties": [{
		"name": "url",
		"value": "samplecompany.in",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "name",
		"value": "samplecompany.in",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}],
	"tags": [],
	"contactIds": [],
	"entiy_group_name": "company",
	"owner_id": 5676618345349120,
	"importedEntity": false,
	"forceCreate": false,
	"companyIds": []
}]
```
	
### 2.7 Add contact to company by contact Id: 
Add contact to company using the contact's Id.
###### Endpoint
POST dev/api/panel/companies/{companyId}/add-contact-by-contactId
###### Required parameters
``companyId`` - Company Id 
``contactId`` - ContactId of the contact

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type:application/x-www-form-urlencoded" \
-d 'companyId=567436789433&contactId=65654657678' \
"https://app.engagebay.com/dev/api/panel/companies/{companyId}/add-contact-by-contactId"
```

### 2.8 Add contact to company using email address: 
Add contact to company using the contact's email address.
###### Endpoint
POST dev/api/panel/companies/{companyId}/add-contact-by-contactEmail
###### Required parameters
``companyId`` - Company Id 
``contactEmail`` - Email Address of the contact

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type:application/x-www-form-urlencoded" \
-d 'companyId=567436789433&contactEmail=samson@walt.ltd' \
"https://app.engagebay.com/dev/api/panel/companies/{companyId}/add-contact-by-contactEmail"
```
### 3.1 Listing deals: 
Returns list of all "Deals" in the domain in JSON format, which are ordered by created time. Paging can be applied using the page_size and cursor query parameters. Cursor for the next page will be in the last deal of the list. If there is no cursor, it means that it is the end of the list.

###### Endpoint
POST dev/api/panel/deals

###### Optional Parameters
- ```page_size``` : Pagesize for paginated results.
- ```sort_key``` :  Sort order for results. Set it to created_time/updated_time to sort list in ascending order. Prepened - to sort in descending.
- ```cursor``` : To get next set of resultset. It will be provided in the last record of previous resultset.
- ```track_id``` : Track ID to list results on specific Track. If No track specified Defaul track results will return. You can find Track ID in Account Settings -> Deal Tracks

###### Example request
```sh
curl  -i -X POST\
-H "Authorization: xxxxxxxxx" \
-H  "Accept:application/json" \
-d "page_size=10&track_id=xxxxx" \
"https://app.engagebay.com/dev/api/panel/deals"
```
######  Example JSON response
```
[{
	"id": 6267486190174208,
	"name": "sample deal",
	"amount": 100,
	"closed_date": 1533126840,
	"track_id": 5151135505580032,
	"milestoneLabelName": "New",
	"tags": [],
	"properties": [],
	"probability": 0.1,
	"owner": {
		"id": 5154169597984768,
		"email": "sample@engagebay.com",
		"name": "sample"
	}
}]
```
### 3.2 Get deal by its ID: 
Gets the deal with the given ID.

###### Endpoint
GET dev/api/panel/deals/{id}

###### Example request
```sh
curl -i -X GET \
 -H "Authorization:xxxxxxxx" \
 -H "Accept:application/json" \
 -H "Content-Type:application/x-www-form-urlencoded" \
"https://app.engagebay.com/dev/api/panel/deals/1234"
```

######  Example JSON response
```
{
	"id": 1234,
	"name": "sample deal",
	"amount": 100,
	"closed_date": 1533126840,
	"track_id": 5151135505580032,
	"milestoneLabelName": "New",
	"tags": [],
	"properties": [],
	"probability": 0.1,
	"owner": {
		"id": 5154169597984768,
		"email": "harry123@yopmail.com",
		"name": "checkharry"
	}
}
```

### 3.3 Create a deal: 
- Accepts deal JSON as data in Post request to the URL specified below. The call returns the deal JSON with id field generated when a new deal is created. If Post data includes valid deal id, the respective deal is updated with the data sent in the request. Milestone name should be same as the one in your account. Please note that it is case sensitive too. (If the milestone name is given incorrectly, it will not be shown in the milestone view.)
- Each field is case sensitive.
- Don't pass null value.
- If you don't know the value of field then don't pass that field at all or pass empty data for the field.

###### Endpoint
POST dev/api/panel/deals/deal

###### Acceptable request representation
```
{
    "name": "sample deal",
    "amount": 100,
    "track_name":"Default",
    "milestoneLabelName":"New"
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "name": "sample deal",
    "amount": 100,
    "track_name":"Default",
    "milestoneLabelName":"New"
}' \
"https://app.engagebay.com/dev/api/panel/deals/deal"
```
###### Example JSON response
#### 
```javascript
{
	"id": 5088020441071616,
	"name": "sample deal",
	"name_sort": "sample deal",
	"amount": 100.0,
	"track_id": 5697266736168960,
	"contact_ids": [],
	"company_ids": [],
	"deal_ids": [],
	"entiy_group_name": "deal",
	"milestoneLabelName": "New",
	"milestoneActualName": "New_Actual",
	"tags": [],
	"properties": [],
	"created_time": 1546938598,
	"probability": 0.1,
	"owner": {
		"id": 5676618345349120,
		"email": "sahith@engagebay.com",
		"name": "sahith",
		"profile_img_url": "https://s3.amazonaws.com/ebuploads2/uploads/1544714031211-sample_png_360p_480x360.png"
	},
	"currency_type": "USD-$",
	"subscribers": [],
	"companies": []
}
```


### 3.4 Delete a deal: 
- Deletes the deal based on the id specified in the url.

###### Endpoint
DELETE dev/api/panel/deals/{id}

###### Example request
```sh
curl -i -X DELETE \
-H "Authorization: xxxxxxxxx" \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/deals/1" 
```

### 3.5 Create deal to a contact using email address:

- Create deal to contact using contact email address.

###### Required parameters

``email`` - Email of contact

###### Endpoint

POST dev/api/panel/deals/create-deal/{email}

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d '{
		"name": "sample deal",
		"amount": 100,
	     "track_name":"Default",
	    "milestoneLabelName":"New"
	}' \
 "https://app.engagebay.com/dev/api/panel/deals/create-deal/test@engagebay.com"
```

###### Example JSON response
#### 
```javascript
{
	"id": 5758313757147136,
	"name": "sample deal",
	"name_sort": "sample deal",
	"amount": 100,
	"track_id": 5697266736168960,
	"contact_ids": [5015780936646656],
	"company_ids": [],
	"deal_ids": [],
	"entiy_group_name": "deal",
	"milestoneLabelName": "New",
	"milestoneActualName": "New_Actual",
	"tags": [],
	"properties": [],
	"created_time": 1542796719,
	"probability": 0.1,
	"owner": {
		"id": 5676618345349120,
		"email": "test12@engagebay.com",
		"name": "tes12"
	},
	"subscribers": [{
		"id": 5015780936646656,
		"email": "test@engagebay.com",
		"name": "test"
	}],
	"companies": []
}
```
### 3.6 Search deals:

- Search using keyword.

###### Required parameters
``q`` - Search keyword (Deal name,amount fields will be searched).
``page_size`` - Number of results to fetch
``type`` - Should be 'Deal' for searching deals

###### Endpoint
GET dev/api/search?q=sampledeal&type=Deal

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxx" \
 "https://app.engagebay.com/dev/api/search?q=sampledeal&type=Deal"
```
###### Example JSON response
```javascript
[{
	"count": 11,
	"id": 5883207295696896,
	"name": "test deal",
	"name_sort": "test deal",
	"amount": 52222,
	"closed_date": 1542883560,
	"track_id": 5697266736168960,
	"contact_ids": [5386679414161408],
	"company_ids": [],
	"deal_ids": [],
	"entiy_group_name": "deal",
	"milestoneLabelName": "New",
	"milestoneActualName": "New_Actual",
	"tags": [{
		"tag": "hi",
		"assigned_time": 1541766966
	}],
	"properties": [{
		"name": "Mobile",
		"value": "",
		"field_type": "NUMBER",
		"is_searchable": true,
		"type": "CUSTOM"
	}, {
		"name": "comments",
		"value": "dfb fgge rhigihrhe bgjer",
		"field_type": "TEXT",
		"is_searchable": true,
		"type": "CUSTOM"
	}],
	"owner_id": 5676618345349120,
	"created_time": 1541674023,
	"probability": 0.1,
	"updated_time": 1542697277,
}]
```

### 3.7 Update deal track: 
Updates the deal with a given track id and milestone name.

###### Endpoint
PUT dev/api/panel/deals/change-track
######  Example JSON response:
```javascript
{
	"id": 5192239399567360,
	"name": "Latest Deal 4",
	"name_sort": "Latest Deal 4",
	"amount": 3000.0,
	"closed_date": 1545436800,
	"track_id": 5697266736168960,
	"contact_ids": [],
	"company_ids": [],
	"deal_ids": [],
	"entiy_group_name": "deal",
	"milestoneLabelName": "New",
	"milestoneActualName": "New_Actual",
	"tags": [{
		"tag": "combine tag3",
		"assigned_time": 1544706319
	}],
	"properties": [{
		"name": "Mobile",
		"value": "",
		"field_type": "NUMBER",
		"is_searchable": true,
		"type": "CUSTOM"
	}],
	"owner_id": 5676618345349120,
	"created_time": 1544188022,
	"probability": 0.1,
	"updated_time": 1544711756,
	"owner": {
		"id": 5676618345349120,
		"email": "sahith@engagebay.com",
		"name": "sahith"
	},
	"currency_type": "USD-$",
	"subscribers": [],
	"companies": []
}
```
###### Example request
```sh
curl -i -X PUT \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
	"id": 5141586283331584,
	"milestoneLabelName" : "New",
	"track_id" : "234412341234"
} ' \
"https://app.engagebay.com/dev/api/panel/deals/change-track"
```

### 3.8 Update properties of a deal by ID (partial update): 
- Updates the properties for a single deal.

We can update the required property fields of the deal using this call. It is used to add a new property or update the existing property. It accepts property object of the deal with a valid parameter in it. Send the ID of the deal to identify it. This will not affect other fields.

Using this API you can not delete properties.

###### Endpoint
PUT dev/api/panel/deals/update-partial

###### Optional parameters
- ``properties`` - Updated custom fields for your deal as object of key/value pairs.

###### Acceptable request representation
```sh
curl -i -X PUT  \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "id": 6218728647688192,
    "properties": [{
		"name": "custom field 1",
		"value": "test",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}]
}' \
"https://app.engagebay.com/dev/api/panel/deals/update-partial"
```

### 4.1 Get all tracks:

- Gets all the tracks.

###### Endpoint

GET dev/api/panel/tracks

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxxxx" \
 "https://app.engagebay.com/dev/api/panel/tracks"
```
###### Example JSON response
```javascript
[{
	"id": 5697266736168960,
	"name": "Default",
	"milestones": [{
		"labelName": "New",
		"labelActualName": "New_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#e2e0e0",
		"probability": 0.1
	}, {
		"labelName": "Prospect",
		"labelActualName": "Prospect_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#c5dec3",
		"probability": 0.2
	}, {
		"labelName": "Proposal",
		"labelActualName": "Proposal_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#c9dde4",
		"probability": 0.3
	}, {
		"labelName": "Won",
		"labelActualName": "Won_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#a6dca2",
		"probability": 1.0
	}, {
		"labelName": "Lost",
		"labelActualName": "Lost_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#e4b5b6",
		"probability": 0.0
	}],
	"isDefault": true,
	"created_time": 1531995775,
	"updated_time": 1540792886
}]
```


### 4.2 Create track:

- Creates a track.

###### Endpoint

POST dev/api/panel/tracks/track

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d \
'{
  "name" : "sampletrack",
  "milestones" : [{"labelName": "New", "labelActualName": "New_Actual", "probability": "0.1", "color": "#e2e0e0"}]
}' \
 "https://app.engagebay.com/dev/api/panel/tracks/track"
```
###### Example JSON response
```javascript
[{
	"id": 5697266736168960,
	"name": "sampletrack",
	"milestones": [{
		"labelName": "New",
		"labelActualName": "New_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#e2e0e0",
		"probability": 0.1
	}],
	"isDefault": false,
    "created_time": 1542786809
}]
```

### 4.3 Update track:

- Updates a track.

###### Endpoint

PUT dev/api/panel/tracks/track

###### Example request
```sh
curl -i -X PUT \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d \
'{
  "id": "5729175541383168",
  "name" : "sample track update",
  "milestones" : [{"labelName": "New", "labelActualName": "New_Actual", "probability": "0.1", "color": "#e2e0e0"}],
  "created_time":"1542786809"
}' \
 "https://app.engagebay.com/dev/api/panel/tracks/track"
```
###### Example JSON response
```javascript
{
	"id": 5729175541383168,
	"name": "sample track update",
	"milestones": [{
		"labelName": "New",
		"labelActualName": "New_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#e2e0e0",
		"probability": 0.1
	}],
	"isDefault": false,
	"created_time": 1542786809,
	"updated_time": 1542788052
}
```
### 4.4 Get track by ID:

- Get track by ID.

###### Endpoint
GET dev/api/panel/tracks/{id}

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxx" \
 "https://app.engagebay.com/dev/api/panel/tracks/5676424065187840"
```
#### Example JSON response

```javascript
{
	"id": 5676424065187840,
	"name": "Default",
	"milestones": [{
		"labelName": "New",
		"labelActualName": "New_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#e2e0e0",
		"probability": 0.1
	}, {
		"labelName": "Prospect",
		"labelActualName": "Prospect_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#c5dec3",
		"probability": 0.2
	}, {
		"labelName": "Proposal",
		"labelActualName": "Proposal_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#c9dde4",
		"probability": 0.3
	}, {
		"labelName": "Won",
		"labelActualName": "Won_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#a6dca2",
		"probability": 1.0
	}, {
		"labelName": "Lost",
		"labelActualName": "Lost_Actual",
		"isWon": false,
		"isLost": false,
		"color": "#e4b5b6",
		"probability": 0.0
	}],
	"isDefault": true,
	"created_time": 1542604315
}
```
### 4.5 Delete track by ID:
- Delete track by ID.

###### Endpoint
DELETE dev/api/panel/tracks/{id}

###### Example request
```sh
curl -i -X DELETE \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxxxx" \
 "https://app.engagebay.com/dev/api/panel/tracks/5676424065187840"
```


### 5.1 Get list of events:

- Fetches the list of events happened in particular time. The start time and end time have to be sent in epoch format as query parameters.

###### Required parameters
``start_time``  - Start time
``end_time`` - End time
``source_type`` - API
 
###### Endpoint

GET dev/api/panel/calendar/event/list?start_time=xxxxx&end_time=xxxxx&source_type=API

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxx" \
 "https://app.engagebay.com/dev/api/panel/calendar/event/list?start_time=1542220200000&end_time=1542824999999&source_type=API"
```
###### Example JSON response
```javascript
[{
	"id": 5288460441092096,
	"owner_id": 5676618345349120,
	"created_time": 1538996150,
	"start_time": 1538998200000,
	"end_time": 1539001799999,
	"user_data": "{\"firstname\":\"sample\",\"lastname\":\"contact\",\"email\":\"samplecontact@gmail.com\"}",
	"color": "#46d6db",
	"name": "60 min",
	"user_time_zone": "Asia/Calcutta",
	"subscriber_id": 4991310645690368,
	"source_type": "WEB",
	"contact_ids": [4991310645690368],
	"company_ids": [],
	"deal_ids": [],
	"event_ids": [],
	"subscribers": [],
	"companies": [],
	"deals": [],
	"owner": {
		"id": 5676618345349120,
		"email": "samplecontact@gmail.com",
		"name": "sample"
	},
	"entiy_group_name": "event"
}]
```

### 5.2 Get events related to contact:

- Retrieves the events related to contact sorted by date.

###### Required parameters
``contact_id``  - Contact ID
 
###### Endpoint

POST dev/api/panel/calendar/event/contact/{contact_id}/events

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d \
   '{
   }' \
   "https://app.engagebay.com/dev/api/panel/calendar/event/contact/5134228568145920/events"
```
###### Example JSON response
```javascript
[{
	"id": 6596436544192512,
	"owner_id": 5676618345349120,
	"created_time": 1542265607,
	"start_time": 1542267000000,
	"end_time": 1542268799999,
	"user_data": "{\"firstname\":\"contactfirst\",\"lastname\":\"lastname\",\"email\":\"samplecontact@engagebay.com\"}",
	"color": "#7ae7bf",
	"name": "30 Minute Meeting",
	"user_time_zone": "Asia/Calcutta",
	"subscriber_id": 5134228568145920,
	"source_type": "WEB",
	"contact_ids": [5134228568145920],
	"company_ids": [],
	"deal_ids": [],
	"event_ids": [],
	"subscribers": [],
	"companies": [],
	"deals": [],
	"entiy_group_name": "event"
}]
```

### 5.3 Create event:

- Creates an event.

###### Required parameters
``contact_id``  - Contact ID
 
###### Endpoint

POST dev/api/panel/calendar/event/normal

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d \
'{
  "name" : "sampleEvent",
  "start_time":"1542868560",
  "end_time":"1542868560",
  "source_type":"API",
  "owner_id":"5676618345349120"
}' \
 "https://app.engagebay.com/dev/api/panel/calendar/event/normal"
```
###### Example JSON response
```javascript
{
	"id": 5270109991993344,
	"owner_id": 5676618345349120,
	"created_time": 1542782746,
	"start_time": 1542868560000,
	"end_time": 1542868560000,
	"name": "sampleEvent",
	"source_type": "API",
	"contact_ids": [],
	"entiy_group_name": "event"
}
```

### 5.4 Update event:

- Updates an event.

###### Endpoint

PUT dev/api/panel/calendar/event/normal

###### Example request
```sh
curl -i -X PUT \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d \
'{
  "id" :"5270109991993344",
  "name" : "sampleEvent",
  "start_time":"1542868560",
  "end_time":"1542868560",
  "source_type":"API",
  "owner_id":"5676618345349120",
  "created_time":"1542782746"
}' \
 "https://app.engagebay.com/dev/api/panel/calendar/event/normal"
```
###### Example JSON response
```javascript
{
	"id": 5270109991993344,
	"owner_id": 5676618345349120,
	"created_time": 1542782746,
	"start_time": 1542868560000,
	"end_time": 1542868560000,
	"name": "sampleEventtest",
	"source_type": "API",
	"contact_ids": [],
	"entiy_group_name": "event"
}
```


### 6.1 Get the list of tasks based on given filters: 
- Returns a list of your tasks based on given filters
```
- Retrives the list of tasks based on the given filters. The filters available are ‘type’,‘status’, and ‘page_size’. These should be sent as a query parameters in the URL.
- taskStatus = one of these values ('not_started','in_progress','waiting','completed','deferred')
- taskType = one of these values ('TODO','EMAIL','CALL')
```
###### Endpoint
POST dev/api/panel/tasks

###### Optional parameters
- ``page_size `` - Pagesize for paginated results.
- ``sort_key`` - Sort order for results. Set it to created_time/updated_time to sort list in ascending order. Prepened - to sort in descending.
- ``cursor`` - To get next set of resultset. You will get this in the last record of previous resultset.

###### Example request
```sh
curl -i -X POST \
   -H "Authorization:xxxxxxxxxxxx" \
   -H "Content-Type:application/x-www-form-urlencoded; charset=UTF-8" \
   -H "Accept:application/json" \
   -d "taskStatus=not_started" \
   -d "taskType=ALL" \
   -d "page_size=10" \
   -d "sort_key=created_time" \
 "https://app.engagebay.com/dev/api/panel/tasks"
```

###### Example JSON response
```javascript
[{
	"id": 4512395720392704,
	"owner_id": 6192449487634432,
	"entiy_group_name": "task",
	"is_due": true,
	"name": "qqqq",
	"description": "",
	"name_sort": "qqqq",
	"type": "TODO",
	"created_time": 1534757461,
	"updated_time": 0,
	"closed_date": 1534757400,
	"task_milestone": "not_started",
	"queue_id": 0,
	"owner": {
		"id": 6192449487634432,
		"email": "sample@engagebay.com",
		"name": "sample"
	}
}]
```
### 6.2 Get the task based on ID: 
- Gets the task with the given ID.

###### Endpoint
GET dev/api/panel/tasks/{id}

###### Example request
```sh
curl -i -X GET \
   -H "Authorization:xxxxxxxxxxxxxx" \
   -H "Accept:application/json" \
   -H "Content-Type:application/x-www-form-urlencoded" \
 "https://app.engagebay.com/dev/api/panel/tasks/5695756786728960"
```

###### Example JSON response
```javascript
{
	"id": 1234,
	"owner_id": 6192449487634432,
	"entiy_group_name": "task",
	"is_due": true,
	"name": "qqqq",
	"description": "",
	"name_sort": "qqqq",
	"type": "TODO",
	"created_time": 1534757461,
	"updated_time": 0,
	"closed_date": 1534757400,
	"task_milestone": "not_started",
	"queue_id": 0,
	"owner": {
		"id": 6192449487634432,
		"email": "sample@engagebay.com",
		"name": "sample"
	}
}
``` : 
- Gets the task with the given ID.

###### Endpoint
GET dev/api/panel/tasks/{id}

###### Example request
```sh
curl https://app.engagebay.com/dev/api/panel/tasks/1234 \
-H "Authorization: xxxxxxxxx" \
-H  "Accept: application/json" -v -u {email}:{API Key}
```

###### Example JSON response
```javascript
{
	"id": 1234,
	"owner_id": 6192449487634432,
	"entiy_group_name": "task",
	"is_due": true,
	"name": "qqqq",
	"description": "",
	"name_sort": "qqqq",
	"type": "TODO",
	"created_time": 1534757461,
	"updated_time": 0,
	"closed_date": 1534757400,
	"task_milestone": "not_started",
	"queue_id": 0,
	"owner": {
		"id": 6192449487634432,
		"email": "sample@engagebay.com",
		"name": "sample"
	}
}
```
### 6.3 Create task: 
- Creates a task 

###### Endpoint
POST dev/api/panel/tasks

###### Example request
```sh
curl -i -X POST \
   -H "Authorization:xxxxxxxxxxx" \
   -H "Accept:application/json" \
   -H "Content-Type:application/json" \
   -d \
'{
	"entiy_group_name": "task",
	"is_due": true,
	"name": "sss4",
	"description": "sss",
	"name_sort": "sss",
	"type": "TODO",
	"updated_time": 0,
	"closed_date": 1535696880,
	"task_milestone": "not_started",
	"queue_id": 0,
	"contact_ids": [],
	"company_ids": [],
	"deal_ids": [],
	"task_ids": [],
	"subscribers": [],
	"companies": [],
	"deals": []
}' \
 "https://app.engagebay.com/dev/api/panel/tasks"
```

###### Example JSON response
```javascript
{
	"id": 4539883511087104,
	"owner_id": 6192449487634432,
	"entiy_group_name": "task",
	"is_due": true,
	"name": "sss",
	"description": "sss",
	"name_sort": "sss",
	"type": "TODO",
	"created_time": 1535696911,
	"updated_time": 0,
	"closed_date": 1535696880,
	"task_milestone": "not_started",
	"queue_id": 0,
	"contact_ids": [],
	"company_ids": [],
	"deal_ids": [],
	"task_ids": [],
	"subscribers": [],
	"companies": [],
	"deals": []
}
```

### 6.4 Update task: 
- Updates task based on its ID

###### Endpoint
PUT dev/api/panel/tasks

######  Acceptable request Representation:
```
{
       "id": 5740495045132288,
	"entiy_group_name": "task",
	"is_due": true,
	"name": "sss4ssss",
	"description": "sssssss",
	"name_sort": "sss",
	"type": "TODO",
	"updated_time": 0,
	"closed_date": 1535696880,
	"task_milestone": "not_started",
	"queue_id": 0,
	"contact_ids": [],
	"company_ids": [],
	"deal_ids": [],
	"task_ids": [],
	"subscribers": [],
	"companies": [],
	"deals": []
}
```

###### Example request
```sh
curl -i -X PUT \
   -H "Authorization:xxxxxxxxxx" \
   -H "Accept:application/json" \
   -H "Content-Type:application/json" \
   -d \
'{
        "id": 5740495045132288,
	"entiy_group_name": "task",
	"is_due": true,
	"name": "sss4ssss",
	"description": "sssssss",
	"name_sort": "sss",
	"type": "TODO",
	"updated_time": 0,
	"closed_date": 1535696880,
	"task_milestone": "not_started",
	"queue_id": 0,
	"contact_ids": [],
	"company_ids": [],
	"deal_ids": [],
	"task_ids": [],
	"subscribers": [],
	"companies": [],
	"deals": []
}' \
 "https://app.engagebay.com/dev/api/panel/tasks"
```
### 6.5 Delete a task based on ID: 

- Delete a task based on its ID

###### Endpoint
DELETE dev/api/panel/tasks/{id}

###### Example request
```sh
curl -i -X DELETE \
   -H "Authorization:xxxxxxxx" \
   -H "Accept:application/json" \
 "https://app.engagebay.com/dev/api/panel/tasks/5147920286351360"
```

### 7.1 Create a note:

- Add note to contacts,companies or deals

###### Required parameters
``subject``  - Subject of the note
``parentId`` - Related contact/company/deal Id
 
###### Endpoint

POST dev/api/panel/notes

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxx" \
   -H "Content-Type:application/json" \
   -d "{}"\
'{"subject": "Engagebay Note", "content": "Engagebay note", "parentId": "5359259403419648"}
' \
 "https://app.engagebay.com/dev/api/panel/notes"
```
###### Example JSON response
```javascript
{
"id":6263278833500160,
"parentId":5359259403419648,
"subject":"Engagebay Note",
"content":"Here you can see",
"type":"PUBLIC",
"created_time":1540531365
}
```

### 8.1 List of forms:
- Get list of forms

###### Endpoint
GET dev/api/panel/forms


###### Example request
```sh
curl -i -X GET \
   -H "Authorization:xxxxxxxxxxx" \
   -H "Accept:application/json" \
 "https://app.engagebay.com/dev/api/panel/forms"
```

###### Example JSON response
```javascript
[{
"id": 5664313465372672,
"name": "\n\t\t\t\t\t Form-25-Jun-18-07:55:00 \n\t\t\t\t",
"alias_name": "\n\t\t\t\t\t form-25-jun-18-07:55:00 \n\t\t\t\t",
"owner_id": 5636470266134528,
"created_time": 1529936702,
"updated_time": 1529936706,
"formHtml": "\n<form class=\"form form-style-form1 \" onsubmit=\"window.parent.EhForm.submit_form(event,this)\" style=\"\n \n background-color:#00afe9;max-width:550px;background-position:0% 0%\">\n\n<fieldset>\n\n<!-- Form Name -->\n<h2 class=\"form-title\" style=\"\"><p>Start Today for Free</p></h2>\n<div class=\"form-description\"><p>consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna</p></div>\n\n\n\n\n\n\n\n<div class=\"form-group\" style=\"color:#333;\">\n \n <div class=\"controls\">\n <input id=\"Email-email\" title=\"\" name=\"email\" type=\"email\" style=\"color:#333;background-color:#fff;\" placeholder=\"Enter your email id\" class=\"form-control\" required=\"true\">\n \n </div>\n</div>\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n<div class=\"form-group\">\n <div>\n <button type=\"submit\" class=\"submit-btn\" style=\"color:#ffffff;background-color:#dc542a;\n \">Get Started</button>\n <br><span id=\"error-msg\"></span>\n </div>\n</div>\n\n</fieldset>\n\n<div class=\"error-success-container\"></div>\n\n<div class=\"form-footer-message\"><p>Incididunt ut labore et dolore magna</p></div>\n\n\n <div class=\"branding-footer\">Powered By <a href=\"https://ehhub.org/openurl?lid=5749921122615296&nid=5726607939469312&c=5700641305395200&b=5677026937667584\" rel=\"nofollow\" target=\"_blank\">EngageBay</a> </div>\n\n\n</form>\n",
"form_attributes": "{\"title_image\":\"\",\"background_image\":\"\",\"background_image_alignment\":\"0% 0%\",\"border_image\":\"\",\"form_background_color\":\"#00afe9\",\"form_size\":\"550px\",\"submit_button_color\":\"#dc542a\",\"submit_button_text_color\":\"#ffffff\",\"submit_button_text\":\"Get Started\",\"redirect_on_subscribe\":\"false\",\"success_message\":\"Success! Now check your email to confirm your submission.\",\"redirect_url\":\"\",\"show_title_image\":false,\"show_background_image\":false,\"show_border_image\":false,\"title\":\"<p>Start Today for Free</p>\",\"description\":\"<p>consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna</p>\",\"footer_text\":\"<p>Incididunt ut labore et dolore magna</p>\",\"form_fields\":[{\"type\":\"email\",\"name\":\"email\",\"title\":\"\",\"pattern\":\"\",\"label\":\"Email\",\"placeholder\":\"Enter your email id\",\"required\":\"true\",\"help_text\":\"\"}]}",
"enable_whitelabel": false,
"form_style": "form1",
"version": "V2",
"incentiveEmail":{"send_incentive": false, "incentive_email_subject": "Important: Confirm your subscription", "incentive_email_message_one": "Thanks for signing up. Click the link below to confirm your subscription and you'll be on your way.",…},
"thumbnail": "https://s3.amazonaws.com/board-uploads/uploads/1529936704700-screenshot.png",
"formStats":{"id": 5734792670740480, "formId": 5664313465372672, "totalVisitors": 0, "uniqueVisitors": 0, "totalContacts": 0,…}
}
]
```
### 8.2 Add contact to a form:

- Add contact to a form

###### Endpoint
POST dev/api/panel/subscribers/add-subscriber-to-form/{subscriber-email}/{formId}

###### Example request

```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -H "Authorization:xxxxxxxxxxxxxxxx" \
   -d \
'{}' \
 "https://app.engagebay.com/dev/api/panel/subscribers/add-subscriber-to-form/sample@engagebay.com/5178895036841984"
```
### 9.1 Add contact to a sequence:

- Add contact to a sequence

###### Endpoint
POST dev/api/panel/subscribers/add-subscriber-to-sequence/{subscriber-email}{sequenceId}

###### Example request

```sh
curl -i -X POST \
    -H "Authorization:xxxxxxxxxxx" \
   -H "Accept:application/json" \
   -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8" \
   -d "{}" \
 	"https://app.engagebay.com/dev/api/panel/subscribers/add-subscriber-to-sequence/sample@engagebay.com/1234"
```

### 10.1 List of lists:
- List of lists

###### Endpoint
GET dev/api/panel/contactlist

###### Example request
```sh
curl -i -X GET \
   -H "Authorization:xxxxxxxx" \
   -H "Accept:application/json" \
 "https://app.engagebay.com/dev/api/panel/contactlist"
```
###### Example JSON response
```javascript
[{
    "rules":[],
    "or_rules":[],
    "id": 5668574207148032,
    "owner_id": 5154169597984768,
    "name": "Default List",
    "created_time": 1527152195,
    "updated_time": 1527152195,
    "owner":{
    "id": 5154169597984768,
    "email": "sample@engagebay.com",
    "name": "engagebay"
    }
}]
```

### 10.2 Add contact to list:

- Add contact to list based on list id
 
###### Endpoint
POST dev/api/panel/contactlist/add-subscriber/{subscriber-email}/{listId}

###### Example request
```sh
curl -i -X POST \
   -H "Authorization:xxxxxxx" \
   -H "Accept:application/json" \
   -d "{}" \
 "https://app.engagebay.com/dev/api/panel/contactlist/add-subscriber/sample@engagebay.com/12356"
```

### 11.1 Get list of owners:

- Get list of all owners.

###### Endpoint

GET dev/api/panel/users

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxx" \
 "https://app.engagebay.com/dev/api/panel/users"
```
###### Example JSON response
```javascript
[{
	"id": 5676618345349120,
	"domain_id": 5641864006860800,
	"email": "engagebayowner@engagebay.com",
	"password_decrypted": "",
	"name": "sahith",
	"created_time": 1529331672,
	"updated_time": 1542787667,
	"is_admin": true,
	"is_verified": true,
	"is_owner": true,
	"job_title": "sales_manager",
	"role": "vice-president-senior-management",
	"phone_number": "+91 88888 88886",
	"language": "en",
	"time_zone": "Asia/Kolkata",
	"time_zone_offset": 330,
	"loggedin_time": 1536128969,
	"misc_info": "{\"country\":\"India\",\"country_code\":\"IN\",\"city\":\"hyderabad\",\"latitude\":\"78.486671\",\"ip_address\":\"183.83.213.105\",\"region\":\"ap\",\"longitude\":\"17.385044\"}",
	"is_signup_process_completed": true,
	"profile_img_url": "https://s3.amazonaws.com/board-uploads/uploads/1531997503373-28279403_116951275800796_612655445084212117_n.jpg",
	"category": "MARKETING",
	"signupSource": "DEFAULT",
	"domainId": 5641864006860800
}]
```
### 12.1 Get list of custom fields:

- Get list of custom fields.

###### Endpoint
GET /dev/api/panel/customfields/list/{type}
###### Required parameters
``type`` - custom field type [CONTACT,DEAL,COMPANY,TICKET].
###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
"https://app.engagebay.com/dev/api/panel/customfields/list/CONTACT"
```
###### Example JSON response
```javascript
[{
	"id": 5718248825815040,
	"field_type": "TEXT",
	"version": "v2",
	"field_label": "Sample Field",
	"field_label_case_sensitive": "Sample Field",
	"saveSilent": false,
	"field_description": "Sample Test Field",
	"field_data": "",
	"is_required": false,
	"is_searchable": true,
	"showInFilter": false,
	"created_time": 1540904183,
	"updated_time": 1549442098,
	"scope": "CONTACT",
	"position": 0,
	"field_name": "Sample_Field"
}]
```

### 12.2 Create a custom field: 
- Accepts custom field JSON as data in Post request to the URL specified below. The call returns the custom field JSON with id field generated when a new custom field is created. If Post data includes valid custom field id, the respective custom field is updated with the data sent in the request.
- Don't pass null value.

###### Required parameters
``scope`` - custom field type must be one of (CONTACT/DEAL/COMPANY/TICKET)
``field_label`` - custom field name.
``field_description`` - custom field description.
``field_type`` - custom field type type must be one of the (TEXT/TEXTAREA/DATE/CHECKBOX/LIST/NUMBER/MULTICHECKBOX)

###### Optional parameters
``is_required`` - To be filled while creating or updating true/false
``is_searchable`` - use  while searching  true/false

###### Endpoint
POST dev/api/panel/customfields/

###### Acceptable request representation
```
{
  "field_label" : "Test field",
  "scope" : "CONTACT",
  "field_description" : "This is Test Field",
  "field_type" : "TEXTAREA",
  "is_required" : "true",
  "is_searchable" : "true"
}
```
###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Content-Type:application/json" \
   -H "Authorization:p5nlcfg7m89a8lb9gf1p1nf6bd" \
   -d \
'{
  "field_label" : "Test field",
  "scope" : "CONTACT",
  "field_description" : "This is Test Field",
  "field_type" : "TEXTAREA",
  "is_required" : "true",
  "is_searchable" : "true"
}' \
 "https://app.engagebay.com/dev/api/panel/customfields/"
```
###### Example JSON response
#### 
```javascript
{
	"id": 6117160669675520,
	"field_type": "TEXTAREA",
	"version": "v2",
	"field_label": "Test field",
	"field_label_case_sensitive": "test field",
	"saveSilent": false,
	"field_description": "This is Test Field",
	"is_required": true,
	"is_searchable": true,
	"showInFilter": false,
	"created_time": 1551444903,
	"updated_time": 1551444903,
	"scope": "CONTACT",
	"position": 11
}
```
### 12.3 Delete a custom field : 

- Delete a custom field

###### Required parameters
``scope``  - scope must be one of (CONTACT/DEAL/COMPANY/TICKET)
``custom-field-id``  - Id of the custom field

###### Endpoint
DELETE  dev/api/panel/customfields/{scope}/{custom-field-id}

###### Example request
```sh
curl -i -X DELETE \
   -H "Accept:application/json" \
   -H "Authorization:p5nlcfg7m89a8lb9gf1p1nf6bd" \
 "https://app.engagebay.com/dev/api/panel/customfields/CONTACT/5718248825815040"
```

### 13.1 Get User Profile : 

- Get User Profile

###### Endpoint
GET  /dev/api/panel/users/profile/user-info

###### Example request
```sh
curl -i -X GET \
   -H "Authorization:p5nlcfg7m89a8lb9gf1p1nf6bd" \
   -H "Accept:application/json" \
 "https://app.engagebay.com/dev/api/panel/users/profile/user-info"
```
###### Example JSON response
#### 
```javascript
{
	"name": "test",
	"email": "test@engagebay.com"
}
```

### 14.1 Get list of tickets:

- Get list of tickets.

###### Endpoint
POST dev/api/panel/tickets

###### Optional parameters
- ``page_size `` - Page size for paginated results.
- ``sort_key`` - Sort order for results. Set it to created_time/updated_time to sort list in ascending order. Prepened - to sort in descending.
- ``cursor`` - To get next set of resultset. You will get it in the last record of previous resultset.

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json"  \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/tickets"
```

###### Example JSON response
```javascript
[
    {
        "id": 1,
        "requester_name": "peter",
        "requester_email": "peter@engagebay.com",
        "subscriber_id": 6179255348101120,
        "subject": "Ticket test subject",
        "source": "DASHBOARD",
        "created_by": "USER",
        "status": 1,
        "priority": 0,
        "type": 0,
        "assigned_to": "GROUP",
        "group_id": 6467327394578432,
        "created_time": 1586862421,
        "is_spam": false,
        "updated_time": 1586862427,
        "public_notes_count": 1,
        "private_notes_count": 0,
        "tags": [],
        "reopens_count": 0,
        "automationStatus": [],
        "html_body": "",
        "last_note_id": 6480521534111744,
        "subscriber": {
            "id": 6179255348101120,
            "email": "peter@engagebay.com",
            "name": "peter"
        },
        "properties": []
    }
]
```

### 14.2 Get list of tickets by filter:

- Get list of tickets by filter.

###### Endpoint
POST dev/api/panel/tickets

###### Optional parameters
- ``filter_id `` - Filter Id for selected view results.
- ``page_size `` - Page size for paginated results.
- ``sort_key`` - Sort order for results.
- ``cursor`` - To get next set of resultset. You will get it in the last record of previous resultset.

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json"  \
-d "{filter_id: 6748802371289088}" \
"https://app.engagebay.com/dev/api/panel/tickets"
```

###### Example JSON response
```javascript
[
    {
        "id": 1,
        "requester_name": "peter",
        "requester_email": "peter@engagebay.com",
        "subscriber_id": 6179255348101120,
        "subject": "Ticket test subject",
        "source": "DASHBOARD",
        "created_by": "USER",
        "status": 1,
        "priority": 0,
        "type": 0,
        "assigned_to": "GROUP",
        "group_id": 6467327394578432,
        "created_time": 1586862421,
        "is_spam": false,
        "updated_time": 1586862427,
        "public_notes_count": 1,
        "private_notes_count": 0,
        "tags": [],
        "reopens_count": 0,
        "automationStatus": [],
        "html_body": "",
        "last_note_id": 6480521534111744,
        "subscriber": {
            "id": 6179255348101120,
            "email": "peter@engagebay.com",
            "name": "peter"
        },
        "properties": []
    }
]
```

### 14.5 Get ticket by ID
Returns data for a single ticket
###### Endpoint
GET /dev/api/panel/tickets/{id}
###### Required parameters
``id`` - Ticket Id.
###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
"https://app.engagebay.com/dev/api/panel/tickets/ticket/{id}"
```
###### Example JSON response
```javascript
{
	"id": 5,
	"requester_name": "Jason Bates",
	"requester_email": "test@engagebay.com",
	"subscriber_id": 6697436372271104,
	"subject": "Test not working ??",
	"status": 1,
	"priority": 2,
	"type": 3,
	"assigned_to": "GROUP",
	"group_id": 5051874215460864,
	"created_time": 1604988043,
	"updated_time": 1604988044,
	"html_body": "",
	"references": [
	  "<20201110060044.1.A19365DDE1FA9367@test.engagebayservice.com>",
	  "<20201110060043.1.E9A4FE223CB884D2@test.engagebayservice.com>"
	],
	"properties": [],
	"forceUpdate": false
	}
```

### 14.3 Create a ticket: 
- Accepts ticket JSON as data in Post request to the URL specified below. The call returns the ticket JSON with id field generated when a new ticket is created.  
- Each field is case sensitive.
- Don't pass null value.
- If you don't know the value of field then don't pass that field at all or pass empty data for the field.

###### Endpoint
POST dev/api/panel/tickets/ticket

###### Acceptable request representation
```
{
    "requester_name": "Sample Contact",
    "requester_email": "ross@gmail.com,
    "subject":"Test not working ??",
    "group_id": "6467327394578432"
    "html_body: "Hello I am testing your docs and find that Test is not working. Please help me"
    "assignee_id": "5358693205934080" // Owner ID of the ticket (Optional)
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "requester_name": "Sample Contact",
    "requester_email": "ross@gmail.com",
    "subject":"Test not working ??",
    "group_id": "6467327394578432",
    "html_body": "Hello I am testing your docs and find that Test is not working. Please help me"
}' \
"https://app.engagebay.com/dev/api/panel/tickets/ticket"
```
###### Example JSON response
#### 
```javascript
{
    "id": 4,
    "requester_name": "Sample Contact",
    "requester_email": "ross@gmail.com",
    "subscriber_id": 5776834092335104,
    "subject": "Test not working ??",
    "source": "DASHBOARD",
    "created_by": "USER",
    "status": 1,
    "priority": 2,
    "type": 3,
    "assigned_to": "GROUP",
    "group_id": 6467327394578432,
    "created_time": 1586867348,
    "is_spam": false,
    "updated_time": 1586867348,
    "public_notes_count": 1,
    "private_notes_count": 0,
    "tags": [],
    "reopens_count": 0,
    "automationStatus": [],
    "html_body": "",
    "references": [],
    "properties": []
}
```

### 14.4 Delete a ticket: 
- Deletes the ticket based on the id specified in the url.

###### Endpoint
DELETE dev/api/panel/tickets/{id}

###### Example request
```sh
curl -i -X DELETE \
-H "Authorization: xxxxxxxxx" \
-d "{}" \
"https://app.engagebay.com/dev/api/panel/tickets/1"
```

### 15.1 List of Tags:
- Get all tags in the account 

###### Endpoint
GET dev/api/panel/tags

###### Example request 
```sh
curl -i -X GET \
   -H "Authorization:xxxxxxxx" \
   -H "Accept:application/json" \
 "https://app.engagebay.com/dev/api/panel/tags"
```
###### Example JSON response
```javascript
[{
	"tag": "Test",
	"created_time": 1589903603
}, {
	"tag": "Test2",
	"created_time": 1591590201
}]
```

### 15.2 Add tag:

- Add new tag to the account. It wont add duplicates if already exists.
 
###### Endpoint
POST dev/api/panel/tags

###### Example request
```sh
curl -i -X POST \
   -H "Authorization:xxxxxxx" \
   -H "Accept:application/json" \
   -d '{
      "tag": "Google"
 }' \
 "https://app.engagebay.com/dev/api/panel/tags"
```


### 16.1 List of products: 
- Returns a list of your products

For the Response in JSON format, add the header 'Accept' as application/json. By default, the response will be in XML format. Paging can be applied using the page_size and cursor query parameters. Cursor for the next page will be in the last product of the list. If there is no cursor, it means that it is the end of list.

###### Endpoint
POST dev/api/panel/products

###### Optional parameters
- ``page_size `` - Page size for paginated results.
- ``sort_key`` - Sort order for results. Set it to created_time/updated_time to sort list in ascending order. 		Prepened - to sort in descending.
- ``cursor`` - To get next set of resultset. You will get it in the last record of previous resultset.

###### Example request
```sh
curl -i -X POST \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json"  \
-d "page_size=10&sort_key=-created_time" \
"https://app.engagebay.com/dev/api/panel/products"
```

###### Example JSON response
```javascript
[
  {
	"id": 6372906833543168,
	"name": "Product Name",
	"description": "Product Description",
	"image_url": "https://d2p078bqz5urf7.cloudfront.net/cloud/assets/img/CART.png",
	"created_time": 1609929740,
	"updated_time": 1609930080,
	"owner_id": 6192449487634432,
	"price": 200,
	"discount_type": "PERCENTAGE",
	"discount": 5,
	"currency": "USD-$",
	"properties": [],
	"cursor": "ClIKFgoMY3JlYXRlZF90aW1lEgYIjKjW_wUSNGoJbm9fYXBwX2lkchQLEgdQcm9kdWN0GICAgICAhKkLDKIBEDUwNjY1NDk1ODA3OTE4MDgYACAB"
	}
]
```

### 16.2 Get product by ID
Returns data for a single product
###### Endpoint
GET /dev/api/panel/products/{id}
###### Required parameters
``id`` - Product Id.
###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
"https://app.engagebay.com/dev/api/panel/products/<productId>"
```
###### Example JSON response
```javascript
{
	"id": 6372906833543168,
	"name": "Product Name",
	"description": "Product Description",
	"image_url": "https://d2p078bqz5urf7.cloudfront.net/cloud/assets/img/CART.png",
	"created_time": 1609929740,
	"updated_time": 1609930080,
	"owner_id": 6192449487634432,
	"price": 200,
	"discount_type": "PERCENTAGE",
	"discount": 5,
	"currency": "USD-$",
	"properties": []
}
```

### 16.3 Creating a product:  

Accepts product JSON as post data along with the credentials of domain User (User name and API Key).
- Each field is case sensitive.
- Please don't pass null value.
- If you don't know value of field then either don't pass that field or pass empty data to a field.

###### Endpoint
POST dev/api/panel/products/product

###### Acceptable request representation:
```
{
	"name": "Product2 Name",
	"description": "Product2 Description",
	"image_url": "https://d2p078bqz5urf7.cloudfront.net/cloud/assets/img/CART.png",
	"owner_id": 6192449487634432,
	"price": 100,
	"discount_type": "AMOUNT",
	"discount": 5,
	"currency": "USD-$"
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
	"name": "Product2 Name",
	"description": "Product2 Description",
	"image_url": "https://d2p078bqz5urf7.cloudfront.net/cloud/assets/img/CART.png",
	"owner_id": 6192449487634432,
	"price": 100,
	"discount_type": "AMOUNT",
	"discount": 5,
	"currency": "USD-$"
}' \
"https://app.engagebay.com/dev/api/panel/products"
```

### 16.4 Update a product by ID: 
- Updates the properties for a single product.

Accepts product JSON as post data along with the credentials of domain User (User name and API Key).
- Each field is case sensitive.
- Please don't pass null value.
- If you don't know value of field then either don't pass that field or pass empty data to a field.

Not: It is entity update. If you miss existing properties, it reset to empty.

###### Endpoint
PUT dev/api/panel/products/product

###### Acceptable request representation
```sh
curl -i -X PUT  \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "id": 6372906833543168,
    "name": "Product2 Name",
	"description": "Product2 Description",
	"image_url": "https://d2p078bqz5urf7.cloudfront.net/cloud/assets/img/CART.png",
	"owner_id": 6192449487634432,
	"price": 150,
	"discount_type": "AMOUNT",
	"discount": 10,
	"currency": "USD-$"
}' \
"https://app.engagebay.com/dev/api/panel/products"
```

### 16.5 Update properties of a product by ID (partial update): 
- Updates the properties for a single product.

We can update the required property fields of the product using this call. It is used to add a new property or update the existing property. It accepts property object of the product with a valid parameter in it. Send the ProductID of the product to identify it. This will not affect other fields.

Using this API you can not delete properties.If subtype is same for phone,website or email then value can be overridden. Lead score, star value and tags can not be updated using this API.

###### Endpoint
PUT dev/api/panel/products/update-partial

###### Optional parameters
- ``properties`` - Updated custom fields for your product as object of key/value pairs.

###### Acceptable request representation
```sh
curl -i -X PUT  \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "id": 6218728647688192,
    "price": "100",
    "name": "name"
    "properties": [{
		"name": "expiry_date",
		"value": "time_in_millis",
		"field_type": "DATE",
		"is_searchable": false,
		"type": "CUSTOM"
	}, {
		"name": "tax",
		"value": "1.0",
		"field_type": "TAX",
		"is_searchable": false,
		"type": "CUSTOM"
	}]
}' \
"https://app.engagebay.com/dev/api/panel/products/update-partial"
```

### 16.6 Get product by Name
Returns data for a single product
###### Endpoint
GET /dev/api/panel/products/getByName/{productName}
###### Required parameters
``productName`` - Product Name.
###### Example request
```sh
curl -i -X GET \
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
"https://app.engagebay.com/dev/api/panel/products/getByName/<productName>"
```
###### Example JSON response
```javascript
{
	"id": 6372906833543168,
	"name": "Product Name",
	"description": "Product Description",
	"image_url": "https://d2p078bqz5urf7.cloudfront.net/cloud/assets/img/CART.png",
	"created_time": 1609929740,
	"updated_time": 1609930080,
	"owner_id": 6192449487634432,
	"price": 200,
	"discount_type": "PERCENTAGE",
	"discount": 5,
	"currency": "USD-$",
	"properties": []
}
```

### 16.7 Delete single product: 
- Delete the single product from account
###### Endpoint
DELETE dev/api/panel/products/{productId}

###### Example Request
```sh
curl -i -X DELETE \
"https://app.engagebay.com/dev/api/panel/products/{productId}"
```

### 16.8 Add a product to contact:  

Add a product to contact with productID. 
- Each field is case sensitive.
- Please don't pass null value.
- If you don't know value of field then either don't pass that field or pass empty data to a field.

###### Endpoint
POST dev/api/panel/products/add-product-to-contact/{contactId}

###### Required parameters
``contactId`` - Contact ID.
``productID`` - Product ID.

###### Acceptable request representation:
```
{
	"productId": "12412123213",
	"isSubscribed": false,
	"subscribedOn": "12123213213",
	"interval": "Monthly"
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
	"productId": "12412123213",
	"isSubscribed": false,
	"subscribedOn": "12123213213",
	"interval": "Monthly"
}' \
"https://app.engagebay.com/dev/api/panel/products/add-product-to-contact/{contactId}"
```

### 16.9 Delete a product from contact:  

Delete a product from contact with productID. 
- Each field is case sensitive.
- Please don't pass null value.
- If you don't know value of field then either don't pass that field or pass empty data to a field.

###### Endpoint
DELETE dev/api/panel/products/delete-product-to-contact/{contactId}/{productId}

###### Required parameters
``contactId`` - Contact ID.
``productID`` - Product ID.

###### Example request
```sh
curl -i -X DELETE \ 
-H "Authorization: xxxxxxxxx" \
"https://app.engagebay.com/dev/api/panel/products/delete-product-to-contact/{contactId}/{productId}"
```

### 17.1 Creating a Broadcast:

Accepts Broadcast JSON as post data along with the credentials of domain User (User name and API Key).
- Each field is case sensitive.
- Please don't pass null value.
- If you don't know value of field then either don't pass that field or pass empty data to a field.
- From Email Address should be a verified one in From Email address in Account Settings.
- Template ID would be the ID in the URL when you open the Email template

###### Endpoint
POST dev/api/panel/bulk-actions/broadcast

###### Acceptable request representation:
```
{
	"emailIds": ["peter@email.com","john@domain.com"],
	"template_id": 12345678,
	"from_email": "from@email.com"
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization: xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
	"emailIds": ["peter@email.com","john@domain.com"],
	"template_id": 12345678,
	"from_email": "from@email.com"
}' \
"https://app.engagebay.com/dev/api/bulk-actions/broadcast"
