---
title: Meeting API Reference

language_tabs:
  - shell
  - javascript

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Meeting Monitor API! You can use our API to access Meeting Monitor API endpoints, which can get information on our the information about meetings/client meetings in our database.


This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

## Login.

You must use the login to access various sort of dashboards from the Meeting Monitor Backend.
The api endpoints will be accessible only after a valid login is done and valid access token is created.

````javascript
var xhttp = new XMLHttpRequest();
var example = {
    "username":"<some random username>",
    "password":"some password"
};
xhttp.open("POST", "http://<Api-base-endpoint>/login", true);
xhttp.send(example);
````
```shell
curl 
    -H "Accept: application/json" 
    -H "Content-type: application/json" 
    -X POST 
    -d '{"username":"<username>","password":"<password>"}' 
    http://<your-base-api-endpoint>/login
```


### Http Request

` POST http://<Api-base-endpoint>/login `

### Request Body

Parameter | Default | Description
--------- | ------- | -----------
username | <not-empty(String)> | Indicates the username of the user.
password | <not-empty(String)> | Indicates the password of the user.

### Response 

```json
{
  "accessToken":"random-string-values",
  "expiresIn":"timeStamp",
  "reloadToken":"token-to-reload-the-auth-token"
}
```

<aside class="notice">
You must store the result access tokens in the localStorage or an device bound database and attach it with every request to access data from the server.
</aside>

# Meetings

## Get All Kittens


```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

# Users

## Get Users
This will give you a list of all the users matching to the string parameter you gave.

```javascript
var xhttp = new XMLHttpRequest();
var userSearch = {
  "searchUser":"<random-substring>"  
};
xhttp.onreadystatechange = function() {
    console.log(JSON.parse(xhttp.responseText));
};
xhttp.open("GET", "http://<Api-base-endpoint>/users", true);
xhttp.setRequestHeader("accessToken","token that is retreived from the inbound database")
xhttp.send(userSearch);
```
```shell
curl 
    -H "Accept: application/json" 
    -H "Content-type: application/json"
    -H "accessToken: random accessToken "
    -X GET 
    -d '{"searchUser":"<non-empty-string>"}' 
    http://<your-base-api-endpoint>/login
```

### Http Request

` GET http://<base-api-endpoint>/users`

### Request Body

Parameter | Default | Description
--------- | ------- | -----------
searchUser | <not-empty(String)> | Indicates the substring of the name of the user.

### Special Request Headers

Header | Default | Description
--------- | ------- | -----------
accessToken | <not-empty(String)> | Indicates the accessToken of the User.


### Response

```json
[
  {
    "name":"string",
    "avatar":"static-file-location",
    "designation":"String",
    "desc":"short-desc"
  }
]
```
