#Server Actions Maintenance

Server actions allow the configuration of actions that will be taken when making calls to the server to update data.  
Simple examples are writing to a log or history table when updating an issue or request or sending an email notification.

NOTE: The current page actions are configured using knowledge of Javascript and will need to be refined to allow 
non-programmers to configure the actions.

[[/images/appfactory/administration/server-actions.png|Server Action Page]]

#####Actions
The type of action to be taken is specified by selecting the action from the 'Actions' select box.  Subsequent data is
specific to the action selected.  Multiple actions are supported for any URL and as many as needed can be specified.

#####Pre/Post Processing
Actions can be specified to occur before or after the URL request processing by checking 'Pre' or 'Post'.  One or both 
checkboxes must be checked.

#####URLs
Actions are associated with server requests by providing the URL for the request.  Specifiying a HTTP method or methods 
will perform the action for requests of the specified method/s.  Leaving the Methods field empty will perform the action 
for all requests to the specified URL.  Wildcards can be used when specifying the URL using Regex notation for the 
wildcard. 

NOTE: The JSON can be formatted to making editing easier.  The JSON structure is checked when clicking the 'REFORMAT'
button or clicking SUBMIT.

[[/images/appfactory/administration/server-actions-json-format.png|Server Action Page]]
