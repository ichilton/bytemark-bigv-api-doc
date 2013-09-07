---
title: 'Introduction'
---

# Introduction

The API is a RESTful and therefore the type of HTTP request determines the action:

 - GET - Read Data
 - POST - Create a new entry
 - PUT - Update an existing entry
 - DELETE - Delete an entry

If you are using curl, you can specify the method with the -X parameter, eg: -X POST

# Data Format

The API uses the JSON data format.

# URL

The endpoint (url) for the API is: https://uk0.bigv.io

# Authentication

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
