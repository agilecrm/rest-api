Authentication :
---------------

This is HTTPS-only API. Authentication will be performed based in the email address of the user and their respective API Key.

Email and API key should be passed via HTTP Basic Authentication. Email address as username and their respective API Key as password.

Endpoints:
----------
All API requests should be made to: https://{domain}.agilecrm.com/dev/

Note: All the data is Case-Sensitive. Emails, names and other values are case sensitive. For example, “Test” and “test” are considered as two different words.

Contacts  & Companies API

|Field Name|Description|Value Type|Read-Only|Mandatory|Accepted values|
|----------:|-----------:|------:|------:|----------:|----------:|
|id|Unique id generated  when contact is created|integer|Yes|Yes, for update and delete calls.|N/A|
|type|Type distinguishes a contact or company.|string|no|No.|Defaults to “PERSON” if not mentioned.“PERSON” or “COMPANY”|
|tags|Unique identifiers added to contact, for easy management of contacts|list|no|no| N/A|
|lead_score|Score of contact|integer|no|no|Any positive integer|
|star_value|Rating of contact (Max value 5)|short|no|no|0 to 5|
|properties|Contact properties are represented by list of JSON objects, each JSON object should follow the prototype shown.  Custom fields will have type as CUSTOM and others will have type SYSTEM.|List of JSON objects|no|first_name is mandator|


###Example

sample jason 
```javascript
{
    	"id": 27001,
    	"type": "PERSON",
    	"created_time": 1349974226,
    	"updated_time": 1364483386,
    	"star_value": 0,
    	"lead_score": 0,
    	"tags": [
        	"Buyer",
        	"Deal Closed"
    	],
    	"properties": [
        	{
            	"type": "SYSTEM",
            	"name": "first_name",
            	"value": "Adam"
        	},
        	{
            	"type": "SYSTEM",
            	"name": "last_name",
            	"value": "Smith"
        	},
        	{
            	"type": "SYSTEM",
            	"name": "company",
            	"value": "Invox"
        	},
        	{
            	"type": "SYSTEM",
            	"name": "title",
            	"value": "Evangelist"
        	},
        	{
            	"type": "SYSTEM",
            	"name": "email",
            	"subtype": "",
            	"value": "jagan@clickdesk.com"
        	},
        	{
            	"type": "CUSTOM",
            	"name": "My Custom Field",
            	"value": "Custom value"
        	}
    	],
    	"widget_properties": "{\"Twitter\":\"11458852\"}",
    	"domainUser": {
        	"id": 314001,
        	"domain": "mycompany",
        	"email": "crm-user@mycompany.com",
        	"is_admin": true,
        	"is_account_owner": false,
        	"is_disabled": false,
        	"name": "angel",
        	"password": "PASSWORD",
        	"info_json_string": "{\"logged_in_time\":1364879569,\"created_time\":1361958281}",
        	"hashedString": "81dc9bdb52d04dc20036dbd8313ed055"
    	}
}```

##Listing Contacts :  
###dev/api/contacts 
Method: GET

Returns list of contacts in domain, which are ordered by creation time

For the Response in the XML format, add the header Accept as application/xml. By default, the response will be in XML format.

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts -H “Accept : application/xml” -v -u {email}:{apikey}```

###Example XML response
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<contacts>
  <contact>
    	<id>40002</id>
    	<type>PERSON</type>
    	<created_time>1356589886</created_time>
    	<updated_time>1357107323</updated_time>
    	<star_value>0</star_value>
    	<lead_score>93</lead_score>
    	<tags>sales</tags>
    	<tags>bruik</tags>
    	<tags>walt</tags>
    	<tags>los</tags>
    	<tags>vo</tags>
    	<tags>steady</tags>
    	<properties>
      		<type>SYSTEM</type>
      		<name>first_name</name>
      		<value>Los </value>
    	</properties>
    <properties>
      	<type>SYSTEM</type>
      	<name>last_name</name>
      	<value>Bruikheilmer</value>
    </properties>
    <properties>
     	<type>SYSTEM</type>
      	<name>company</name>
      	<value>steady.inc</value>
    </properties>
    <properties>
      	<type>SYSTEM</type>
      	<name>title</name>
      	<value>VP Sales</value>
    </properties>
    <properties>
      	<type>SYSTEM</type>
      	<name>email</name>
      	<subtype>work<subtype/>
      	<value>bruik@walt.inc</value>
    </properties>
   <properties>
      	<type>SYSTEM</type>
      	<name>address</name>
      	<value>{"address":"","city":"","state":"","zip":"","country":""}</value>
    </properties>
    <domainUser>
<id>106010</id>
      	<domain>yaswanth</domain>
      	<email>praveen@invox.com</email>
      	<is_admin>true</is_admin>
      	<is_account_owner>true</is_account_owner>
      	<is_disabled>false</is_disabled>
      	<name>yaswanth</name>
      	<password>PASSWORD</password>
<info_json_string>
{"logged_in_time":1359434638,"created_time":1358831084}
</info_json_string>
    </domainUser>
   </contact>
</contacts>
```
For the Response in the JSON format, add the header Accept as application/json.

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts -H “Accept : application/json” 
-v -u {email}:{apikey}
```
####Example JSON response
```javascript
[
      {
        "count": "9",
        "id": "40002",
        "type": "PERSON",
        "created_time": "1356589886",
        "updated_time": "1357107323",
        "star_value": "0",
        "lead_score": "93",
        "tags": [
          "sales",  "bruik", "walt", "los",  "vo",  "steady"
        ],
        "properties": [
          {
            "type": "SYSTEM",
            "name": "first_name",
            "value": "Los "
          },
          {
            "type": "SYSTEM",
            "name": "last_name",
            "value": "Bruikheilmer"
          },
          {
            "type": "SYSTEM",
            "name": "company",
            "value": "steady.inc"
          },
          {
            "type": "SYSTEM",
            "name": "title",
            "value": "VP Sales"
          },
          {
            "type": "SYSTEM",
            "name": "email",
            "subtype": "work",
            "value": "bruik@walt.inc"
          },
          {
            "type": "SYSTEM",
            "name": "address",
            "value": "{\"address\":\"\",\"city\":\"\",\"state\":\"\",\"zip\":\"\",\"country\":\"\"}"
          }
        ],
        "domainUser": {
          "id": "106010",
          "domain": "yaswanth",
          "email": "praveen@invox.com",
          "is_admin": "true",
          "is_account_owner": "true",
          "is_disabled": "false",
          "name": "yaswanth",
          "password": "PASSWORD",
          "info_json_string": "{\"logged_in_time\":1359434638,\"created_time\":1358831084}"
        }
      },
      {
        "id": "41002",
        "type": "PERSON",
        "created_time": "1356590542",
        "updated_time": "1359367255",
        "star_value": "4",
        "lead_score": "92",
        "tags": [
          "president",
          "john",
          "doe",
          "cruzzetech"
        ],
        "properties": [
          {
            "type": "SYSTEM",
            "name": "first_name",
            "value": "John"
          },
          {
            "type": "SYSTEM",
            "name": "last_name",
            "value": "Doe"
          },
          {
            "type": "SYSTEM",
            "name": "company",
            "value": "cruzzetech.com"
          },
          {
            "type": "SYSTEM",
            "name": "email",
            "value": "john@cruzzetech.com"
          },
          {
            "type": "SYSTEM",
            "name": "title",
            "value": "President"
          }
        ],
"tags_with_time_json": "{\"president\":1359365229885,\"john\":1359365229885,\"doe\":1359365229885,\"cruzzetech\":1359365229885}",
        "domainUser": {
          "id": "106010",
          "domain": "yaswanth",
          "email": "praveen@invox.com",
          "is_admin": "true",
          "is_account_owner": "true",
          "is_disabled": "false",
          "name": "yaswanth",
          "password": "PASSWORD",
          "info_json_string": "{\"logged_in_time\":1359434638,\"created_time\":1358831084}"
        }
      }
    ]
```

###Other available Responses:
Status 200: Gives the above JSON object in above format.
Status 401: Unauthorised. When the user name and password fields are wrong.

##Get contact by id
###dev/api/contacts/{id}
Method: GET 

Returns contact object which is associated given id

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts/{id} -H “Accept :application/xml” 
-v -u {email}:{apikey}
```
###Example Response

Returns created contact object with all parameters in it as mentioned in the above example. 

###Other available Responses:
Status 200: Gives the above JSON object in above format.
Status 401: Unauthorised. When the user name and password fields are wrong.

##Creating a contact
###dev/api/contacts
Method: POST

Accepts contact JSON as post data along with the credentials of domain User (User name and API Key).

###Acceptable request Representation:
```javascript
{      
"star_value": "4",
      "lead_score": "92",
      "tags": ["Lead","Likely Buyer","You_can-user $special chars"],
       "properties": [
           {
               "type": "SYSTEM",
               "name": "first_name",
               "value": "Los "
           },
           {
               "type": "SYSTEM",
               "name": "last_name",
               "value": "Bruikheilmer"
           },
          {
            "type": "SYSTEM",
            "name": "company",
            "value": "steady.inc"
          },
          {
            "type": "SYSTEM",
            "name": "title",
            "value": "VP Sales"
          },
          {
            "type": "SYSTEM",
            "name": "email",
            "subtype": "work",
            "value": "bruik@walt.inc"
          },
          {
            "type": "SYSTEM",
            "name": "address",
            "value": "{\"address\":\"\",\"city\":\"\",\"state\":\"\",\"zip\":\"\",\"country\":\"\"}"
          },
          {
            	"type": "CUSTOM",
            	"name": "My Custom Field",
            	"value": "Custom value"
        	}

        ]
  }
```

###Response:
Status 200: Contact added successfully. Returns the newly added contact object in the response.
Status 401: Unauthorised. When the user name and password fields are wrong.
Status 400: If the input is in wrong format.
Status 406: If the Limit of the contacts exceeded.

##Updating contact
###dev/api/contacts
Method: PUT 


Accepts contact object with valid id parameter in it, where ‘id’  refers the contact to be updated.

###Acceptable request Representation:
```javascript
{      
	“id”:8573489754593
"star_value": "4",
      "lead_score": "92",
      "tags": ["Lead","Likely Buyer","You_can-user $special chars"],
       "properties": [
           {
               "type": "SYSTEM",
               "name": "first_name",
               "value": "Los "
           },
           {
               "type": "SYSTEM",
               "name": "last_name",
               "value": "Bruikheilmer"
           },
          {
            "type": "SYSTEM",
            "name": "company",
            "value": "steady.inc"
          },
          {
            "type": "SYSTEM",
            "name": "title",
            "value": "VP Sales"
          },
          {
            "type": "SYSTEM",
            "name": "email",
            "subtype": "work",
            "value": "bruik@walt.inc"
          },
          {
            "type": "SYSTEM",
            "name": "address",
            "value": "{\"address\":\"\",\"city\":\"\",\"state\":\"\",\"zip\":\"\",\"country\":\"\"}"
          },
          {
            	"type": "CUSTOM",
            	"name": "My Custom Field",
            	"value": "Custom value"
        	}

        ]
  }
```

If there is no ID, it will considered as a new contact.

###Response:
Status 200: Contact updated successfully. Returns the updated contact object in the response.
Status 401: Unauthorised. When the user name and password fields are wrong.
Status 400: If the input is in wrong format.

##Delete single contact
###dev/api/contacts/{id}
Method: DELETE
	Deletes contact based on the id of the contact, which is  sent in request url path.
	
###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts/{id}  \
-v -u {email}:{apikey} -X DELETE
```

###Response:
Status 204: Contact deleted successfully.
Status 401: Unauthorised. When the user name and password fields are wrong.

##Search Contact by Email
###dev/api/contacts/search/email
Method: POST

Searches for the contact with given email address. Email address should be sent as a form parameter(Content-Type: application/x-www-form-urlencoded ). We can search for multiple contacts using their Email-Id’s.

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts/search/email -H "Accept: application/xml"
-H “Content-Type :application/x-www-form-urlencoded” 
-d ‘email_ids=["notifications@basecamp.com"]’
-v -u {email}:{apikey} -X POST
```

###Response:
Status 200: Gives the Contact as JSON object in above format. If email doesn’t match, it will return an empty object.
Status 401: Unauthorised. When the user name and password fields are wrong.
Status 400: If the email is in wrong format.

##Adding Tags to a contact based on Email:
###dev/api/contacts/email/tags/add
Method: POST

Searches for the contact based on the given email address and add the given tags to the contact. You can add multiple tags. Tags should be sent as a array. Email address (email) and tags (tags) array should be sent as a form parameter(Content-Type: application/x-www-form-urlencoded )

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts/email/tags/add -H "Accept: application/xml"
-H “Content-Type :application/x-www-form-urlencoded” 
-d ‘email=notifications@basecamp.com&tags=[“testing”]’
-v -u {email}:{apikey} -X POST
```
###Response:
Status 204: Tags added successfully.
Status 401: Unauthorised. When the user name and password fields are wrong.
Status 400: If the input is in wrong format.

##Delete Tags to a contact based on Email:
###dev/api/contacts/email/tags/delete
Method: POST

Searches for the contact based on the given email address and search for the given tag in the contact tags list. If the there is, then delete that tag. You can delete multiple tags. Tags should be sent as a array. Email address (email) and tags (tags) array should be sent as a form parameter(Content-Type: application/x-www-form-urlencoded )

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts/email/tags/delete -H "Accept: application/xml"
-H “Content-Type :application/x-www-form-urlencoded” 
-d ‘email=notifications@basecamp.com&tags=[“testing”]’
-v -u {email}:{apikey} -X POST
```
###Response:
Status 204: Tags deleted successfully.
Status 401: Unauthorised. When the user name and password fields are wrong.
Status 400: If the input is in wrong format.

##Add Score to a Contact using Email-ID:
###dev/api/contacts/add-score
Method: POST

It is used to change the score of the contact by using the email address. If we want to decrease a quantity from the existing score, then use negative values for the score parameter.

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts/add-score -H "Accept: application/xml" -H “Content-Type :application/x-www-form-urlencoded” 
-d ‘email=notifications@basecamp.com&score=5’ -v -u {email}:{apikey} -X POST
```
###Response:
Status 200: Score changed successfully and returns the Contact object.
Status 401: Unauthorised. When the user name and password fields are wrong.
Status 400: If the input is in wrong format

##Get Tasks related to Contact:
###dev/api/contacts/{contact_id}/tasks/sort
Method: GET

Retrieve the tasks related to contact sorted on the date (Latest first.).

###Using curl
```sh
curl https://{domain}.agilecrm.com/dev/api/contacts/{contact_id}/tasks/sort -H "Accept: application/xml" -v -u {email}:{apikey}
```
###Response:
Status 200: Returns the task list related to the contact.
```javascript
[
    {
        "id": 5152971570544640,
        "type": "EMAIL",
        "priority_type": "NORMAL",
        "due": 1409596200,
        "created_time": 1409567774,
        "is_complete": false,
        "contacts": [
            {
                "id": 5716606839685120,
                "type": "PERSON",
                "created_time": 1403057154,
                "updated_time": 1403057154,
                "viewed_time": 0,
                "viewed": {
                    "viewed_time": 1409567737463,
                    "viewer_id": 5345980119515136
                },
                "star_value": 0,
                "lead_score": 0,
                "tags": [],
                "tagsWithTime": [],
                "properties": [
                    {
                        "type": "SYSTEM",
                        "name": "first_name",
                        "value": "Basecamp (2Desk)"
                    },
                    {
                        "type": "SYSTEM",
                        "name": "last_name",
                        "value": "Basecamp (2Desk)"
                    },
                    {
                        "type": "SYSTEM",
                        "name": "email",
                        "value": "notifications@basecamp.com"
                    }
                ],
                "campaignStatus": [],
                "entity_type": "contact_entity",
                "unsubscribeStatus": [],
                "emailBounceStatus": [],
                "owner": {
                    "id": 5345980119515136,
                    "domain": "prabathk",
                    "email": "prabath.kolipaka@gmail.com",
                    "is_admin": true,
                    "is_account_owner": true,
                    "is_disabled": false,
                    "name": "prabath kolipaka"
                }
            }
        ],
        "subject": "Contact created in agile crm",
        "entity_type": "task",
        "notes": [],
        "progress": 0,
        "status": "YET_TO_START",
        "ownerPic": "https://s3.amazonaws.com/agilecrm/panel/uploaded-logo/1401427105618?id=upload-container",
        "taskOwner": {
            "id": 5345980119515136,
            "domain": "prabathk",
            "email": "prabath.kolipaka@gmail.com",
            "is_admin": true,
            "is_account_owner": true,
            "is_disabled": false,
            "name": "prabath kolipaka"
        }
    }
]
```
Status 401: Unauthorised. When the user name and password fields are wrong.


