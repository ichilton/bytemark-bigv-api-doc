---
title: 'Authentication'
---

# Authentication

The API currently uses HTTP Basic authentication (over SSL). The username and
password are sent with each request.

If you are not familiar with HTTP Basic authentication, you take the username and password, separated by a colon (i.e: username:password) and base64 encode it. You then supply a header as follows (replace auth_string_here with the base64 encoded string you just created).

```
Authorization: Basic auth_string_here
```

If you are using something like curl, you can use the -u parameter to supply a username/password and it will send the correct header for you.

Yubikeys are sent as a HTTP header: X-Yubikey-Otp: <output of keypress>
- again, this needs to be sent with every request.

The privilege model determines how long a particular yubikey will be
accepted for; by default, you can replay the same OTP over and over for
15 minutes before it becomes invalid and a new one needs to be used.

If you are using a user who's privileges do not require a Yubikey, you can ignore this header - it doesn't need to be supplied. In fact, if it is, it will be ignored if it's not required.
