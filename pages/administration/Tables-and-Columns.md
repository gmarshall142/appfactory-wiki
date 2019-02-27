# Table and Column Maintenance

Application tables and table columns are defined and maintained on this page.  All data tables have an application ID 
column which specifies that the data belongs to the specified application.  Once tables and their columns are defined they can be used as application resources and/or as the data source for an application form.

Tables are one of four types:

1. Lookup - an existing system lookup table (Activity, Status, Priority, Issue Type, etc.)
2. Issue - an existing issue  table that has a combination of predefined columns and columns added for the application.
3. Custom Lookup - a custom lookup table with ID, Label, and Description columns.
4. Custom Table - a custom table with completely custom columns.

[[/images/appfactory/administration/tables-add.png|Add table type]]

 Application tables and columns are displayed in the ‘Tables’ dropdown on the right side of the page.  Both tables and 
 columns are edited by selecting them in the dropdown, editing them in the forms, and submitting the changes.

[[/images/appfactory/administration/tables.png|Table list and detail]]

Columns can be references to lookup tables or data stored as JSON in a json column.  When a table is created some 
columns are generated automatically for the specific table type.  Additional columns can be added to customize the table
 for the application.

[[/images/appfactory/administration/column-add.png|Add column]]
