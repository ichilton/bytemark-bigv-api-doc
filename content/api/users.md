---
title: 'Users'
---

# Users

## Introduction 

Users generally relate to physical people. Each person who needs to access BigV will generally have a single user. Users can be granted access to multiple accounts.

To understand how this fits with accounts, groups and privileges, see the "Accounts, Users, Privileges and Groups" section on [the intro page](/notes/intro).

More information about BigV users can be found here: [http://www.bigv.io/support/howto/user/](http://www.bigv.io/support/howto/user/)


## Endpoints

    GET    /users     # all users
    GET    /users/ID  # single user
    POST   /users     # create
    PUT    /users/ID  # update
    DELETE /users/ID  # delete

ID should be replaced with a user id or username.


## Attributes

* **id** - Unique id for this user (numeric)
* **username** - Unique username for this user - must only contain letters or numbers
* **email** - User's e-mail address
* **authorized_keys** - SSH public key's
* **password** - only used when creating (or updating) a user - it's not returned in when reading users


## Authentication

Users can be created (using POST) without authentication.

If the request has no authentication, it will also accept an account_name parameter and create an account at the same time.


## Examples

#### All Users

##### Request:

    GET /users

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/users

##### Response:

    [{"id":1,"username":"myusername","email":"me@mydomain.com","authorized_keys":"ssh-rsa AAAAsdjkhfkshfkjshdfkhjsdfkjhdskjfhsdkjhfiusdfyiusdyfiydsuifysduiyfiusdyfidsyfiusydifuysdiufyiudsyfisduyfiudsyfuisdhfkjsdnkjhaskjdhkashdkjashdkasndaisudyasudyisadhjnasjdnkjsandkjasndkjanskdnaskndkasjd== me@myhost.com\n\n"}]

#### Single User

##### Request:

    GET /users/myusername

##### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/users/myusername

##### Response:

    {"id":1,"username":"myusername","email":"me@mydomain.com","authorized_keys":"ssh-rsa AAAAsdjkhfkshfkjshdfkhjsdfkjhdskjfhsdkjhfiusdfyiusdyfiydsuifysduiyfiusdyfidsyfiusydifuysdiufyiudsyfisduyfiudsyfuisdhfkjsdnkjhaskjdhkashdkjashdkasndaisudyasudyisadhjnasjdnkjsandkjasndkjanskdnaskndkasjd== me@myhost.com\n\n"}


#### Create New User:

##### Request:

    POST /users

##### Curl:
    openssl passwd -1 "plaintextpassword"

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         -X POST \
         -d '{"username":"mynewusername","email":"me@mydomain.com","password":"password_hash_from_above_here"}' \
         https://uk0.bigv.io/users

##### Response:

    {"id":2,"username":"mynewusername","email":"me@mydomain.com","authorized_keys":null}


