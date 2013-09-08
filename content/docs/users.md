---
title: 'Users'
---

# Users

## Introduction 

An account can have multiple users, which would usually relate to physical people you would like to be able to access your BigV account.

More information about BigV users can be found here: [http://www.bigv.io/support/howto/user/](http://www.bigv.io/support/howto/user/)


## Fields

* id - Unique id for this user (numeric)
* username - Unique username for this user - must only contain letters or numbers
* email - User's e-mail address
* authorized_keys - SSH public key's
* password - only used when creating (or updating) a user - it's not returned in when reading users

## Examples

#### All Users

##### Request:

    GET /users

#### Curl:

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

#### Curl:

    curl -H "Content-type: application/json" \
         -H "X-Yubikey-Otp: output_from_key_here" \
         -sslv3 \
         -u username_here:password_here \
         https://uk0.bigv.io/users/myusername

##### Response:

    {"id":1,"username":"myusername","email":"me@mydomain.com","authorized_keys":"ssh-rsa AAAAsdjkhfkshfkjshdfkhjsdfkjhdskjfhsdkjhfiusdfyiusdyfiydsuifysduiyfiusdyfidsyfiusydifuysdiufyiudsyfisduyfiudsyfuisdhfkjsdnkjhaskjdhkashdkjashdkasndaisudyasudyisadhjnasjdnkjsandkjasndkjanskdnaskndkasjd== me@myhost.com\n\n"}


#### Create New Account:

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


