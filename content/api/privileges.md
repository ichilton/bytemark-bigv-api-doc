---
title: 'Privileges'
---

# Privileges (Work In Progress)


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

* id
* username
* level
* creating_username
* yubikey_required
* yubikey_otp_max_age
* ip_restrictions
* virtual_machine_id
* group_id
* account_id


## Examples

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/users/myusername/privileges


    [{"id":1,"level":"account_admin","yubikey_required":true,"yubikey_otp_max_age":900,"ip_restrictions":null,"username":"myusername","_links":{"self":{"href":"/privileges/25"},"user":{"href":"/users/25"},"account":{"href":"/accounts/24","title":"Account myaccountname"}},"account_id":1},{"id":5273,"level":"account_admin","yubikey_required":true,"yubikey_otp_max_age":900,"ip_restrictions":null,"username":"myusername","_links":{"self":{"href":"/privileges/5273"},"user":{"href":"/users/25"},"account":{"href":"/accounts/5114","title":"Account myotheraccount"}},"account_id":2}]