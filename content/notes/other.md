---
title: 'Introduction'
---

#General Notes & HTTP Response Codes

Query string parameters will be ignored, except for the view=overview parameter, on certain calls. This embeds other related information into the response to save making HTTP calls. Note though that not all fields are necessarily included in overview mode - i.e it's possible that you can get more data on the included records by making a specific API call for that resource.

Sometimes you will be able to use GET on a resource, but will get a 403 if you try to PUT/POST/DELETE to it without having appropriate permissions. If you cannot use GET on the resource, then GET/PUT/POST/DELETE will all return HTTP response code: 404 Not Found.

Requests for unknown resources return HTTP response code: 404 Not Found.

Unexpected errors or server-side problems will return HTTP response code: 500.

The body content for PUT and POST requests is a JSON hash of attribute => value (eg: {"username":"something"}) for the attributes you would like to update. Unknown attributes are silently discarded. Bad values for known attributes will cause the request to fail with HTTP response code: 400. In this case, the response body will be a JSON hash of attr => [error1, ...].

Successful POST requests return HTTP response code: 201 (200 for PUT) and the response body will be a JSON hash describing the newly created (or updated) resource.

Successful GET requests return HTTP 200 and the response body is a JSON hash or array of hashes describing the resource, or resources, requested.

Successful DELETE requests return HTTP 204 (No Content). If a delete fails, a 400 response with a text/plain or application/json body (whichever is most appropriate) will be returned with the reason.

All requests should set Accept and Content-Type headers appropriately. If Content-Type is set incorrectly, POST and PUT will not work.
