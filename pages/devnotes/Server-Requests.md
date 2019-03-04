#Server Requests

###Overview
Server Requests allow an actions (notification, logging, debugging, capture history record, etc) with a server request 
REST api call.  There are two steps in providing this functionality:
* Annotate or decorate server API functions with processing that provides additional processing to the existing function.  
This is 'aspect oriented programming' providing common features across multiple REST functions.  This is also referred to 
as 'cross-cutting concerns'.  In this case the common feature is attachment of additional processing before or after the
REST request is processed. 
>Current Implementation: The api for a form record (fetch, add, update) have an actionProcessing decorator. 
* Define the type of action and associate it with a REST request and map the data used in the additional processing to 
the data that exists in the REST query.
>Current Implementation: The request/action are associated and configured in the [Server Request Actions 
Maintenance](Server-Request-Actions(Server Request Maintenance)) screen.

###Event Attributes
1. Action - This is the action that will be performed such as database update, logging, email notification, debugging 
call.  Processing for each action is done by a mixture of fixed coding and JSON configuration data that provides the 
specifics of the data that is processed.
2. Pre / Post Processing - When the processing will take place; before the REST call, after the REST call, or both.
3. URL - The request url supporting regex wildcards.  For each call to the actionProcessing method (based on @actionProcessing
decorator) the url being called is checked for a match as defined in the urlactions table.  This information is cached so
the first call will execute the query and cached information will be returned in subsequent calls.
4. Methods - The specific method calls that should be processed for the URL or NULL for all requests.
5. Action Data - The JSON specification of the event specific data.  This allows the mapping of data from the server 
request to the data used in the action processing.
6. Template - The template provides the text to be populated with data and used during the processing.
>Current Implementation: Text sent during a notification using {{}} to specify data elements that will be replaced.
 

####History JSON
* table - apptables.id for the table that is being queried
* action - 'add'
* columns - array of objects with 'id', 'type', 'attribute' attributes
  * id - appcolumns.id for the data element
  * type - where in the request data object that the data can be found; 'data', 'state', 'request'
  * attribute - data element name

Example:  
```javascript
{
    "table": 121,
    "action": "add",
    "columns": [
        {
            "id": 485,
            "type": "data",
            "attribute": "id"
        },
        {
            "id": 486,
            "type": "state",
            "attribute": "stateinid"
        },
        {
            "id": 487,
            "type": "state",
            "attribute": "stateoutid"
        },
        {
            "id": 490,
            "type": "request",
            "attribute": "details"
        }
    ]
}
```
####Email JSON
* table - apptables.id for the table that is being queried
* columns - array of objects with 'id', 'type', 'attribute' attributes
  * id - appcolumns.id for the data element
  * type - where in the request data object that the data can be found; 'data', 'state', 'request'
  * attribute - data element name
####Email Template
``` javascript
All,

Subject: {{subject}}

Updated: {{updatedat}}
Activity: {{activity}}
Status: {{status}}
Priority: {{priority}}
```

###Request Query Data
Currently only appformController requests support actionProcessing extensions.  The add and update processing extends the
data available for post processing by doing the following:
1. Returns an extended query using the procedure __formRecordFindById__ which returns the record and data from referenced 
lookup tables.
2. Captures state processing requests that are done when updating an 'issue' table.  The add call queries the __workflow_states__
table to get the initial state information and the update call queries the __workflow_statetransisions__ to get the current
state information.
3. Captures the initial request form data (key,value,fieldid) and makes it part of the data returned.
