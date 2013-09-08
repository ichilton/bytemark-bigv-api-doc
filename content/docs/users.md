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
