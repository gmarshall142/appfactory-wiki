# Application Access and Users/Groups/Roles

## Users
A single table is provided for all users in the system and is based on the VTAMP users' table.  The intention is to re-use user information across applications, but in order to reference the USERS table in the application it is necessary to create a virtual table reference to it for an application which allows the table to be referenced and used as a resource to populate lists.

## Groups
Groups can be created for re-use in defining sets of users that can then be assigned to application roles.  The primary use of groups is to define user sets that belong to organizations and perform common tasks.  The USERS and GROUPS tables are linked using the USERGROUPS table.

## Roles
Roles are created for an application.  Users and Groups can then be assigned roles in the ROLEASSIGNMENTS table.

A resource can be created in an application allowing users to be listed in forms.  
> NOTE: Currently all roles and users/groups that are members of those roles are listed in the resource.  It will be necessary to provide role resources and filtering using specific roles within an application.

[[/images/app-users/users-groups-roles.png|Users Groups and Roles Tables]]



