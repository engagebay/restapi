EngageBay REST API
=================
[EngageBay](https://www.engagebay.com/) is a simple, affordable all-in-one marketing and sales software built for growing businesses. Get the power of an enterprise software at a fraction of the cost.

### Overview
API is in active development. Currently it allows you to access:
- Contacts
- Companies
- Deals
- Tasks
- Notes
- Forms
- Sequences
- Events
- Tracks
- Owners

### Authentication
This is an HTTPS-only API.

All API calls require ```Authorization``` header. You should pass REST API Key as a header value.

###### API Key
You can find your API Key in the EngageBay Account Admin Settings -> API -> API Key.

###### End Points
All API requests should be made to: https://app.engagebay.com/dev/

Note: All data is case-sensitive. Emails, names and other values are case sensitive. For example, "Test" and "test" are considered two different words.

### Getting Started

**[Contacts](#1-contacts---companies-api)**
* [1 Listing contacts](#11-listing-contacts)
* [2 Get contact by ID](#12-get-contact-by-id)
* [3 Creating a contact](#13-creating-a-contact-)
* [4 Updating contact](#14-updating-contact-)
* [5 Delete single contact](#15-delete-single-contact-)
* [6 Adding tags to a contact based on email](#16-adding-tags-to-a-contact-based-on-email-)
* [7 Delete tags to a contact based on email](#17-delete-tags-to-a-contact-based-on-email-)
* [8 List tags for a contact](#18-list-tags-for-a-contact-)
* [9 Add score to a contact using email ID](#19-add-score-to-a-contact-using-email-id-)
* [10 Search contacts/companies/deals](#110-search-contactscompaniesdeals)
* [11 Delete tags value by ID](#111-delete-tags-value-by-id)
* [12 Change contact owner](#112-change-contact-owner)

**[Company APIs](#21-creating-a-company)**

* [1 Creating a company](#21-creating-a-company-)
* [2 Updating a company](#22-updating-a-company-)
* [3 Get list of companies](#23-get-list-of-companies-)
* [4 Get company by id](#24-get-company-by-id-)
* [5 Delete single company](#25-delete-single-company-)

**[Deals](#31-listing-deals)**

* [1 Listing deals](#31-listing-deals-)
* [2 Get deal by its ID](#32-get-deal-by-its-id-)
* [3 Create deal](#33-create-a-deal)
* [4 Delete deal](#34-delete-deal-)
* [5 Create deal to a contact using emailID](#35-create-deal-to-a-contact-using-emailid)

  

**[Tasks](#41-listing-tasks)**

* [1 Get the list of tasks based on given filters](#41-get-the-list-of-tasks-based-on-given-filters-)
* [2 Get the task based on ID](#42-get-the-task-based-on-id-)
* [3 Create task](#43-create-task-)
* [4 Update task](#44-update-task-)
* [5 Delete a task based on ID](#45-delete-a-task-based-on-id-)


**[Forms](#51-listing-forms)**

* [1 List of forms](#51-list-of-forms-)
* [2 Add contact to a form](#52-add-contact-to-a-form)

**[Sequences](#61-add-contact-to-a-sequence-)**

* [1 Add contact to a sequence](#61-add-contact-to-a-sequence-)

**[Lists](#71-list-of-lists-)**

* [1 List of lists](#71-list-of-lists-)
* [2 Add contact to list](#72-add-contact-to-list-)


**[Notes](#81-create-a-note)**
* [1 Create a note](#81-create-a-note)


**[Events](#91-get-list-of-events)**

* [1 Get list of events](#91-get-list-of-events)
* [2 Get events related to contact](#92-get-events-related-to-contact)
* [3 Create event](#93-create-event)
* [4 Update event](#94-update-event)

**[Tracks](#101-get-list-of-tracks)**

* [1 Get all the tracks](#101-get-all-the-tracks)
* [3 Create track](#102-create-track)
* [4 Update track](#103-update-track)
* [5 Get track by ID](#104-get-track-by-id)
* [6 Delete track by ID](#105-delete-track-by-id)

**[Owners](#111-get-list-of-owners)**

* [1 Get list of owners](#111-get-list-of-owners)



### 1.1 Listing contacts: 
- Returns a list of your contacts

For the Response in JSON format, add the header 'Accept' as application/json. By default, the response will be in XML format. Paging can be applied using the page_size and cursor query parameters. Count of the contacts will be in the first contact and Cursor for the next page will be in the last contact of the list. If there is no cursor, it means that it is the end of list.

###### Endpoint
POST dev/api/panel/subscribers

###### Optional parameters
- ``page_size `` - Page size for paginated results.
- ``sort_key`` - Sort order for results.
- ``cursor`` - To get next set of resultset. You will get it in the last record of previous resultset.

###### Example request
```sh
curl -i -X POST \
-H "Authorization : xxxxxxxxx" \
-H "Accept : application/json"  \
-d "{}" \
'https://app.engagebay.com/dev/api/panel/subscribers'
```

###### Example JSON response
```javascript
[
  {
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
},{
	"cursor": "Cl0KFgoMY3JlYXRlZF90aW1lEgYI2IWV3AUSP2oRYWNjb3VudGJveC0xNTQ2MDVyFwsSClN1YnNjcmliZXIYgICAgIDAowgMogEQNTYyOTQ5OTUzNDIxMzEyMBgAIAE",
	"id": 4659730278514688,
	"owner_id": 6192449487634432,
	"name": "Test contact 2",
	"firstname": "Test contact",
	"lastname": "2",
	"fullname": "Test contact 2",
	"name_sort": "test",
	"email": "test@engagebay.com",
	"created_time": 1535460056,
	"updated_time": 1535529626,
	"status": "UNCONFIRMED",
	"sources": [{
		"type": "DEFAULT",
		"subscribed_on": 1535460056,
		"status": "ACTIVE",
		"custom": 0
	}],
	"companyIds": [],
	"contactIds": [],
	"properties": [{
		"name": "name",
		"value": "test contact",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "last_name",
		"value": "2",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "email",
		"value": "test@engagebay.com",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "phone",
		"value": "",
		"field_type": "TEXT",
		"is_searchable": false,
		"type": "SYSTEM"
	}, {
		"name": "country",
		"value": "",
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
	"tags": [],
	"broadcastIds": [6084697348112384],
	"openedLinks": [],
	"emailProperties": [{
		"emailDbId": 6119881720201216,
		"entityId": 6084697348112384,
		"sentAt": 1535529626,
		"status": "SENT_6084697348112384"
	}],
	"unsubscribeList": [],
	"emailBounceStatus": [],
	"importedEntity": false,
	"forceCreate": false,
	"forceUpdate": false,
	"score": 5
}]
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
-H "Authorization : xxxxxxxxx" \
-H "Accept : application/json" \
'https://app.engagebay.com/dev/api/panel/subscribers/1'
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
### 1.3 Creating a contact :  

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
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization : xxxxxxxxx" \
-H "Accept : application/json" \
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
'https://app.engagebay.com/dev/api/panel/subscribers/subscriber'
```
### 1.4 Updating contact : 
- Updates the information for a single contact.

We can update the required property fields of the contact using this call. It is used to add a new property or update the existing property. It accepts property object of the contact with a valid parameter in it. Send the ContactId of the contact to identify it. This will not affect other fields.

###### Endpoint
PUT dev/api/panel/subscribers/subscriber

###### Optional parameters
- ``first_name``- Updated first name for the contact.
- ``properties`` - Updated custom fields for your contact as object of key/value pairs.

###### Acceptable request representation
```sh
curl -i -X PUT  \
-H "Authorization : xxxxxxxxx" \
-H "Accept : application/json" \
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
'https://app.engagebay.com/dev/api/panel/subscribers/subscriber'
```
### 1.5 Delete single contact : 
- Delete the single contact from account
###### Endpoint
DELETE dev/api/panel/subscribers/{contact-id}

###### Example Request
```sh
curl -i -X DELETE \
'https://app.engagebay.com/dev/api/panel/subscribers/{contact-id}'
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
-H "Authorization : xxxxxxxxx" \
-H "Content-Type :application/x-www-form-urlencoded" \
-d 'email=samson@engagebay.com&tags=["testsample"]' \
'https://app.engagebay.com/dev/api/panel/subscribers/email/tags/add'
```
### 1.7 Delete tags to a contact based on email: 
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
-H "Authorization : xxxxxxxxx" \
-H "Content-Type :application/x-www-form-urlencoded" \
-d 'email=sample@engagebay.com&tags=["sampletest"]' \
'https://app.engagebay.com/dev/api/contacts/email/tags/delete '
```

### 1.8 List tags for a contact: 
Lists all the tags for a contact
###### Endpoint
POST dev/api/panel/subscribers/get-tags/{subscriber-email}
###### Required parameters
``Email`` - Email address of the contact

###### Example request
```sh
curl -i -X POST \
-H "Authorization : xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type :application/x-www-form-urlencoded" \
-d "{}" \
'https://app.engagebay.com/dev/api/panel/subscribers/get-tags/{subscriber-email}' 
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
-H "Authorization : xxxxxxxxx" \
-H "Accept: application/json" \
-H "Content-Type :application/x-www-form-urlencoded" \
-d 'email=samson@walt.ltd&score=100' \
'https://app.engagebay.com/dev/api/panel/subscribers/add-score'
```

### 1.10 Search contacts/companies/deals:

- Search using keyword.

###### Required parameters
``q`` - Search keyword (all contact/company/deal default fields and searchable custom fields will be searched).
``page_size`` - Number of results to fetch
``type`` - Should be 'Subscriber' for searching Contacts, 'Company' for Companies and 'Deal' for Deals 

###### Endpoint
GET dev/api/search?q=searchtext&type=Subscriber

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxx" \
 'https://app.engagebay.com/dev/api/search?q=test&type=Subscriber'
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
### 1.11 Delete tags value by ID:

- Delete tag values by contact id.

###### Required parameters

``contactId`` - ID of the contact.
``tags`` - List of tags to delete

###### Endpoint

POST dev/api/panel/subscribers/contact/tags/delete

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxx" \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -d "contactId=5015780936646656" \
   -d "tags=[\"testtag\"]" \
 'https://app.engagebay.com/dev/api/panel/subscribers/contact/tags/delete'
```

### 1.12 Change contact owner:

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
 'https://app.engagebay.com/dev/api/panel/subscribers/update-owner-by-email?subscriberId=5015780936646656&ownerEmail=test@engagebay.com'
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
-H "Authorization : xxxxxxxxx" \
-H "Accept : application/json" \
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
'https://app.engagebay.com/dev/api/panel/companies/company'
```
### 2.2 Updating a company: 
We can update required property fields of the company using this call. It is used to add a new property or update the existing property. It accepts property object of company with valid parameter in it. Send the Company-Id of the company to identify it. This will not affect other fields.

###### Endpoint
PUT dev/api/panel/companies/company
######  Acceptable request representation:
```javascript
{
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
	"companyIds": []
}
```
###### Example request
```sh
curl -i -X PUT \ 
-H "Authorization : xxxxxxxxx" \
-H "Accept : application/json" \
-H "Content-Type: application/json" \
-d '{
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
	"companyIds": []
} ' \
'https://app.engagebay.com/dev/api/panel/companies/company'
```
### 2.3 Get list of companies : 
- Get list of companies

Fetches the list of companies. Page_size, sort_key and cursor should be sent as a form parameter (Content-Type: application/x-www-form-urlencoded). Paging can be applied using the page_size and cursor form parameters. Cursor for the next page will be in the last company of the list. If there is no cursor, it means that it is the end of the list.

###### Endpoint
POST dev/api/panel/companies

###### Example request
```sh
curl -i -X POST \
-H "Authorization : xxxxxxxxx" \
-H "Accept: application/json" \
-d "{}" \
'https://app.engagebay.com/dev/api/panel/companies'
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
### 2.4 Get company by ID : 
- Returns company object which is associated with given company id

###### Endpoint
GET dev/api/panel/companies/{id}

###### Example request
```sh
curl -i -X GET \
-H "Authorization : xxxxxxxxx" \
-H "Accept :application/json" 
'https://app.engagebay.com/dev/api/panel/companies/{id}'
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

### 2.5 Delete a single company: 
- Deletes company based on the id of the company, which is sent in the request URL path.

###### Endpoint
DELETE dev/api/panel/companies/{id}

###### Example request
```sh
curl -i -X DELETE  \
-H "Authorization : xxxxxxxxx" \
'https://app.engagebay.com/dev/api/panel/companies/{id}' 
```

### 3.1 Listing deals : 
Returns list of all "Deals" in the domain in JSON format, which are ordered by created time. Paging can be applied using the page_size and cursor query parameters. Count of the deals will be in the first deal and the cursor for the next page will be in the last deal of the list. If there is no cursor, it means that it is the end of the list.

###### Endpoint
POST dev/api/panel/deals

###### Optional Parameters
```page_size``` : Pagesize for paginated results.
```sort_key``` :  Sort order for results.
```cursor``` : To get next set of resultset. It will be provided in the last record of previous resultset.

###### Example request
```sh
curl  -i -X POST\
-H "Authorization : xxxxxxxxx" \
-H  "Accept:application/json" \
-d "{}" \
'https://app.engagebay.com/dev/api/panel/deals'
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
	}]
```
### 3.2 Get deal by its ID : 
Gets the deal with the given ID.

###### Endpoint
GET dev/api/panel/deals/{id}

###### Example request
```sh
curl -i -X GET \
 -H "Authorization:e4au70gjkttb7kh7i5h1q3qb4u" \
 -H "Accept:application/json" \
 -H "Content-Type:application/x-www-form-urlencoded" \
'https://app.engagebay.com/dev/api/panel/deals/1234'
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
	"name_sort": "sample deal",
	"amount": 100,
        "track_id":"5697266736168960",
        "milestoneActualName" :"New_Actual",
        "milestoneLabelName":"New",
	"tags": [],
	"properties": []
}
```
###### Example request
```sh
curl -i -X POST \ 
-H "Authorization : xxxxxxxxx" \
-H "Accept : application/json" \
-H "Content-Type: application/json" \
-d '{
	"name": "sample deal",
	"name_sort": "sample deal",
	"amount": 100,
        "track_id":"5697266736168960",
        "milestoneActualName" :"New_Actual",
        "milestoneLabelName":"New",
	"tags": [],
	"properties": []
}' \
'https://app.engagebay.com/dev/api/panel/deals/deal'
```
### 3.4 Delete deal: 
- Deletes the deal based on the id specified in the url.

###### Endpoint
POST dev/api/panel/deals/{id}

###### Example request
```sh
curl -i -X POST \
-H "Authorization : xxxxxxxxx" \
-d "{}" \
'https://app.engagebay.com/dev/api/panel/deals/1' 
```

### 3.5 Create deal to a contact using emailID:

- Create deal to contact using contact email Id.

###### Required parameters

``email`` - Email of contact

###### Endpoint

POST dev/api/panel/create-deal/{email}

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxx" \
   -H "Content-Type:application/json" \
 'https://app.engagebay.com/dev/api/panel/dev/api/panel/create-deal/test@engagebay.com'
```
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

### 4.1 Get the list of tasks based on given filters: 
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
- ``sort_key`` - Sort order for results.
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
 'https://app.engagebay.com/dev/api/panel/tasks'
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
### 4.2 Get the task based on ID: 
- Gets the task with the given ID.

###### Endpoint
GET dev/api/panel/tasks/{id}

###### Example request
```sh
curl -i -X GET \
   -H "Authorization:xxxxxxxxxxxxxx" \
   -H "Accept:application/json" \
   -H "Content-Type:application/x-www-form-urlencoded" \
 'https://app.engagebay.com/dev/api/panel/tasks/5695756786728960'
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
-H "Authorization : xxxxxxxxx" \
-H  "Accept : application/json" -v -u {email}:{API Key}
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
### 4.3 Create a task: 
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
 'https://app.engagebay.com/dev/api/panel/tasks'
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

### 4.4 Update task: 
- Update a task based on its ID

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
 'https://app.engagebay.com/dev/api/panel/tasks'
```
### 4.5 Delete a task based on ID: 
- Delete a task based on its ID

###### Endpoint
DELETE dev/api/panel/tasks/{id}

###### Example request
```sh
curl -i -X DELETE \
   -H "Authorization:e4au70gjkttb7kh7i5h1q3qb4u" \
   -H "Accept:application/json" \
 'https://app.engagebay.com/dev/api/panel/tasks/5147920286351360'
```
### 5.1 List of forms:
- Get list of forms

###### Endpoint
GET dev/api/panel/forms


###### Example request
```sh
curl -i -X GET \
   -H "Authorization:xxxxxxxxxxx" \
   -H "Accept:application/json" \
 'https://app.engagebay.com/dev/api/panel/forms'
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
### 5.2 Add contact to a form:

- Add contact to a form

###### Endpoint
POST dev/api/panel/subscribers/add-subscriber-to-form/{subscriber-email}/{formId}

###### Example request
```sh
curl https://app.engagebay.com/dev/api/panel/subscribers/add-subscriber-to-form/sample@engagebay.com/1234  \
   -H "Authorization:xxxxxxxxxxx" \
   -H "Accept:application/json" \
   -H Content-Type: application/json; charset=utf-8" \
   -v -u sample@engagebay.com:123456 
```

### 6.1 Add contact to a sequence:

- Add contact to a sequence

###### Endpoint
POST dev/api/panel/subscribers/add-subscriber-to-sequence/{subscriber-email}{sequenceId}

###### Example request
```sh
curl https://app.engagebay.com/dev/api/panel/subscribers/add-subscriber-to-sequence/sample@engagebay.com/1234  \
   -H "Authorization:xxxxxxxxxxx" \
   -H "Accept:application/json" \
   -H Content-Type: application/json; charset=utf-8" \
   -v -u sample@engagebay.com:123456 
```

### 7.1 List of lists:
- List of lists

###### Endpoint
GET dev/api/panel/contactlist

###### Example request
```sh
curl -i -X GET \
   -H "Authorization:e4au70gjkttb7kh7i5h1q3qb4u" \
   -H "Accept:application/json" \
 'https://app.engagebay.com/dev/api/panel/contactlist'
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

### 7.2 Add contact to list:

- Add contact to list based on list id
 
###### Endpoint
POST dev/api/panel/contactlist/add-subscriber/{subscriber-email}/{listId}

###### Example request
```sh
curl -i -X POST \
   -H "Authorization:xxxxxxx" \
   -H "Accept:application/json" \
   -d "{}" \
 'https://app.engagebay.com/dev/api/panel/contactlist/add-subscriber/sample@engagebay.com/12356'
```

### 8.1 Create a note:

- Add note to contacts,companies or deals

###### Required parameters
``subject``  - Subject of the note
``parentId`` - Related contact/company/deal Id
 
###### Endpoint

POST dev/api/panel/dev/api/panel/notes

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxx" \
   -H "Content-Type:application/json" \
   -d "{}"\
'{"subject": "Engagebay Note", "content": "Engagebay note", "parentId": "5359259403419648"}
' \
 'https://app.engagebay.com/dev/api/panel/notes'
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

### 9.1 Get list of events:

- Fetches the list of events happened in particular time. The start time and end time have to be sent in epoch format as query parameters.

###### Required parameters
``start_time``  - Start time
``end_time`` - End time
``source_type`` - API
 
###### Endpoint

GET dev/api/panel/dev/api/calendar/event/list?start_time=xxxxx&end_time=xxxxx&source_type=API

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxx" \
 'https://app.engagebay.com/dev/api/panel/dev/api/calendar/event/list?start_time=1542220200000&end_time=1542824999999&source_type=API'
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

### 9.2 Get events related to contact:

- Retrieves the events related to contact sorted by date.

###### Required parameters
``contact_id``  - Contact ID
 
###### Endpoint

POST dev/api/panel/dev/api/calendar/event/contact/{contact_id}/events

###### Example request
```sh
curl -i -X POST \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxx" \
   -H "Content-Type:application/json" \
   -d \
   '{
   }' \
   'https://app.engagebay.com/dev/api/calendar/event/contact/5134228568145920/events'
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

### 9.3 Create event:

- Creates an event.

###### Required parameters
``contact_id``  - Contact ID
 
###### Endpoint

POST dev/api/calendar/event/normal

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
 'https://app.engagebay.com/dev/api/calendar/event/normal'
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

### 9.4 Update event:

- Updates an event.

###### Endpoint

PUT dev/api/panel/dev/api/calendar/event/normal

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
 'https://app.engagebay.com/dev/api/calendar/event/normal'
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

### 10.1 Get all the tracks:

- Gets all the tracks.

###### Endpoint

GET dev/api/panel/dev/api/panel/tracks

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxxxx" \
 'https://app.engagebay.com/dev/api/panel/tracks'
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


### 10.2 Create track:

- Creates a track.

###### Endpoint

POST dev/api/panel/dev/api/panel/tracks/track

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
 'https://app.engagebay.com/dev/api/panel/tracks/track'
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

### 10.3 Update track:

- Updates a track.

###### Endpoint

PUT dev/api/panel/dev/api/panel/tracks/track

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
 'https://app.engagebay.com/dev/api/panel/tracks/track'
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
### 10.4 Get track by ID:

- Get track by ID.

###### Endpoint
GET dev/api/panel/tracks/{id}

###### Example request
```sh
curl -i -X GET \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxx" \
 'https://app.engagebay.com/dev/api/panel/tracks/5676424065187840'
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
### 10.5 Delete track by ID:
- Delete track by ID.

###### Endpoint
DELETE dev/api/panel/tracks/{id}

###### Example request
```sh
curl -i -X DELETE \
   -H "Accept:application/json" \
   -H "Authorization:xxxxxxxxxxxxxxxx" \
 'https://app.engagebay.com/dev/api/panel/tracks/5676424065187840'
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
 'https://app.engagebay.com/dev/api/panel/users'
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
