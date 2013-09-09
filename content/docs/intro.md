---
title: 'Introduction'
---

# Introduction

The API is a RESTful and therefore the type of HTTP request determines the action:

 - GET - Read Data
 - POST - Create a new entry
 - PUT - Update an existing entry
 - DELETE - Delete an entry

If you are using curl, you can specify the method with the -X parameter, eg: -X POST, -X PUT and -X DELETE.

See the examples in each section for more information about this.


## Data Format

The API uses the JSON data format.


## URL

The endpoint (url) for the API is: https://uk0.bigv.io


## Authentication

The API currently uses HTTP Basic authentication (over SSL). Username and
password sent with each request.

If you are not familiar with HTTP Basic authentication, you take the username and password, separated by a colon (i.e: username:password) and base64 encode it. You then supply a header as follows (replace auth_string_here with the base64 encoded string you just created).

Authorization: Basic auth_string_here

If you are using something like curl, you can use the -u parameter to supply a username/password and it will send the correct header for you.

Yubikeys are sent as a HTTP header: X-Yubikey-Otp: <output of keypress>
- again, this is sent with every request at the moment.

The privilege model determines how long a particular yubikey will be
accepted for; by default, you can replay the same OTP over and over for
15 minutes before it is invalidated.

If you are using a user who's privileges do not require a Yubikey, you can ignore this header - it doesn't need to be supplied. In fact, if it is, it will be ignored if it's not required.


## General Notes & HTTP Response Codes

Query string parameters will be ignored, except for the view=overview parameter. This embeds other related information into the response to save making HTTP calls. Note though that not all fields are necessarily included in overview mode.

Sometimes you will be able to GET a resource, but will get a 403 if you try to PUT/POST/DELETE it without having appropriate
permissions. If you cannot GET the resource, then GET/PUT/POST/DELETE will all return HTTP response code: 404.

Requests for unknown resources return HTTP response code: 404.

Unexpected errors or server-side problems will return HTTP response code: 500.

The body content for PUT and POST requests is a JSON hash of attribute => value (eg: {"username":"something"}) for the attributes you would like to update. Unknown attributes are silently discarded. Bad values for known attributes will cause the request to fail with HTTP response code: 400. In this case, the response body will be a JSON hash of attr => [error1, ...].

Successful POST requests return HTTP response code: 201 (200 for PUT) and the response body will be a JSON hash describing the newly created (or updated) resource.

Successful GET requests return HTTP 200 and the response body is a JSON hash or array of hashes describing the resource, or resources, requested.

Successful DELETE requests return HTTP 204 (No Content). If a delete fails, a 400 response with a text/plain or application/json body (whichever is most appropriate) will be returned with the reason.

All requests should set Accept and Content-Type headers appropriately. If Content-Type is set incorrectly, POST and PUT will not work.


## Accounts, Users, Privileges and Groups

Use of all of these terms can seem a little confusing at first, but it's actually quite simple once you get your head around how things are structured and what each one is for.

Users generally relate to physical people. Each person who needs to access BigV will generally have a single user. Users can be granted access to multiple accounts.

Accounts are a billable entity. Accounts would generally relate to a company, organisation, or maybe a persion. An account can be accessed by multiple users (eg: employees) and a user can access multiple accounts (so the same user could for example, access the accounts of multiple companies and/or have a personal account). Accounts contain groups and virtual machines.

Groups are quite simply a collection of virtual machines. By default, each account contains a single group called 'default' and new virtual machines will be added to that group. You can however create more groups of your choosing to group collections of virtual machines. You can then give other users control of those groups, intead of the whole account where you might not want them to have access to everything, or individual virtual machines which would be tedious if you had a lot and multiple users.

Privileges define if (and under what conditions) a user can access either an account, a group or a virtual machine. For example, a user could be an account admin for an account under the same name, if they know their password and have a yubikey - or know their password and are coming from a certain ip address. The same user could also be the account admin for a different account if they know their password and have a yubikey. They could then be allowed to access a certain group of machines from another account just by providing their password.
