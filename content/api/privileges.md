---
title: 'Privileges'
---

# Privileges


## Introduction

Privileges define if (and under what conditions) a user can access either an account, a group or a virtual machine. For example, a user could be an account admin for an account under the same name, if they know their password and have a yubikey - or know their password and are coming from a certain ip address. The same user could also be the account admin for a different account if they know their password and have a yubikey. They could then be allowed to access a certain group of machines from another account just by providing their password.

To understand how this fits with accounts, groups and users, see the "Accounts, Users, Privileges and Groups" section on [the intro page](/notes/intro).

More information about BigV Privileges can be found here: [http://www.bigv.io/support/howto/privilege/](http://www.bigv.io/support/howto/privilege/)


## Endpoints

    GET    /privileges     # all privileges (for current user)
    GET    /privileges/ID  # single privilege
    PUT    /privileges/ID  # update
    DELETE /privileges/ID  # delete

    POST   /users/USER_ID/privileges  # create privileges for user
    GET    /users/USER_ID/privileges  # all privileges for user

USER_ID should be replaced with a user id or username and ID with the privilege id.


## Attributes

* **id** - unique key (integer).
* **username** - username this privilege is for.
* **level** - the level of privilege (see below).
* **creating_username** - username of the user who created this user.
* **yubikey_required** - boolean specifying whether a yubikey is required for access.
* **yubikey_otp_max_age** - how long the yubikey value will be accepted for (in seconds).
* **ip_restrictions** - whether the user has to be accessing from certain ip addresses to have this privilege.

One of the following:

* **virtual_machine_id**
* **group_id**
* **account_id**

The valid levels are:

* cluster_su
* cluster_admin
* account_admin 
* group_admin
* vm_admin
* vm_console

Users can only create or modify privileges which have a lower level than themselves.

i.e account_admin's (the default level users have on their account) can only create/modify group_admin, vm_admin and vm_console privileges, not their own or other account_admins. They would have to contact support for that.

Once created, only yubikey_required, yubikey_otp_max_age and ip_restrictions can be updated.


## Examples

#### All privileges for a user

##### Request:

    GET /users/myusername/privileges

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -u username_here:password_here \
         https://uk0.bigv.io/users/myusername/privileges

##### Response:

    [{"id":1,"level":"account_admin","yubikey_required":true,"yubikey_otp_max_age":900,"ip_restrictions":null,"username":"myusername","_links":{"self":{"href":"/privileges/25"},"user":{"href":"/users/25"},"account":{"href":"/accounts/24","title":"Account myaccountname"}},"account_id":1},{"id":5273,"level":"account_admin","yubikey_required":true,"yubikey_otp_max_age":900,"ip_restrictions":null,"username":"myusername","_links":{"self":{"href":"/privileges/5273"},"user":{"href":"/users/25"},"account":{"href":"/accounts/5114","title":"Account myotheraccount"}},"account_id":2}]
