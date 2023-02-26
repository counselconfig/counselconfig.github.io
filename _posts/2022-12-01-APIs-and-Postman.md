---
layout: post
title: RESTful APIs and Postman
tags: API RESTful endpoint
---

### API in basic terms 

An Application Programing Interface (API) is essentially a well defined method of communicating with a 'service'. This means that a service provides a server to which a request can be sent and the server will answer with well defined responses, in accordance with an API specification. 

### REST API

A representational state transfer (REST) API has an architecture which when compliant with REST contraints are coined RESTful, making use of web standards like HTML, JSON XML. 

I said this would be a basic discusion, so all that we should know about RESTful APIs is that there are four types of actions that are used to communicate with it. 


* ```GET```: A get action means we ask the service for data - we will check this out later. 

* ```POST```: This action is typically used to create data in the service. 

* ```PUT```: This action is used to update already existing data

* ```DELETE```: This action is used to delete existing data

### Sending parameters and arguments to a RESTful service. 

A REST request typically has three parts: The URL we are sending the request to, the HEADER of the request (which normally holds basic properties of the request), and in the BODY of the request. 



* For examples of arguments sent in the URL, a ```GET``` action sent to a website selling cats at <ins>www.catsforsale.co.uk/user/1234</ins> could be a way to ask for information about user with 1234, and if we also want a list of all their cats 🐱, we might do so by sending the ```GET``` request to <ins>www.catsforsale.co.uk/user/1234?include_cats=true</ins>. 

* The header is sent along with the request - normally, in a browser, the request header is unseen since it is managed by the browser. Now, this is where <a target='_blank' rel='noopener' href='https://www.postman.com/'>Postman</a> comes in handy as it lwil let us edit the header. 



### Postman

I will demonstrate ```GET``` requests with Postman using two real APIs, namely SmartSurvey and Eventbrite.

### SmartSurvey API

The SmartSurvey API does not require  extra HEADER parameters, which means it be queried using a browser of a preference. Two authentication keys are needed to send a 'call' this service, viz: an 'api_token', and an 'api_token_secret', to let the server know the query can be trusted by an authenticated user. The a target='_blank' rel='noopener' href='https://docs.smartsurvey.io/docs'>Smart Survey documentation</a> explains how to obtain these tokens. 

There are two endpoints with the SmartSurvey API 

**1. https://api.smartsurvey.io/v1/surveys**

The first endpoint above returns a list of all the surveys created. It requires the “api_token” and “api_token_secret” as parameters and two optional parameters for paginating the result: 

```page_size``` - this specifies how many service should be returned in each call. 

```page``` - this specifies which page to return. 

i.e. if ```page_size=100```, and ```page=1```, we get the first 100 surveys. Changing page to page=2 gets us the next 100 surveys and so forth. If ```page_size``` and ```page``` are not specified we get 1 survey (the latest). Note this service does not use the header, we can test this in any browser, for example: 


<a target='_blank' rel='noopener' href='https://api.smartsurvey.io/v1/surveys?api_token=[api_token]&api_token_secret=[api_token_secret]&page_size=100&page=1'>https://api.smartsurvey.io/v1/surveys?api_token=[api_token]&api_token_secret=[api_token_secret]&page_size=100&page=1</a>

**2. https://api.smartsurvey.io/v1/surveys/[survey_id]/responses**

The second type above returns all  responses to the specific survey specified by the ```survey_id```. It takes the same parameters as previously listed (```api_token```, ```api_token_secret```, ```page_size``` and ```page```). It also takes an extra parameter ```include_labels``` - this should be set as ```true``` as without it the questions and responses will be absent with only question and answer IDs present) e.g. to get the first 100 survey responses for survey ID 421142, open the following link in a browser:

<a target='_blank' rel='noopener' href='https://api.smartsurvey.io/v1/surveys/421142/responses?api_token=[api_token]&api_token_secret=[api_token_secret]&include_labels=true&page_size=100&page=1'>https://api.smartsurvey.io/v1/surveys/421142/responses?api_token=[api_token]&api_token_secret=[api_token_secret]&include_labels=true&page_size=100&page=1</a>


#### Query SmartSurvey API with Postman

1. Add URL request in the URL text field with the “action” on the left is set to ```GET```) and press send!


<embed src='/assets/images/ss_postman.png' width='100%' height='100%' style='display: block; margin: 0 auto'>


#### SmartSurvey API Basic Authentication

SmartSurvey supported querystring parameters as exampled above but as of today these are now deprecated and all requests should switch to using Basic Auth. Instead of adding the API Token and Token Secret as parameters in the GET request URL, they take the form of a ```username``` and ```password``` respectively, which are passed to the header instead à la below: 

<a target='_blank' rel='noopener' href='https://api.smartsurvey.io/v1/surveys/421142/responses?include_labels=true&page_size=100&page=1'>https://api.smartsurvey.io/v1/surveys/421142/responses?include_labels=true&page_size=100&page=1</a>


### Eventbrite API

This is the <a target='_blank' rel='noopener' href='eventbrite.com/platform/api'>documentation for the Eventbrite API</a>. Authentication in Eventbrite differs from Smart Survey as it is achieved by sending the authentication keys in the ```HEADER```, which means we need to use Postman by adding a key-value pair in the “Headers” tab, with: 

* ```Key``` = “Authorization”
* ```Value``` = “Bearer [private token]”

Check the documetion on how to retrieve your private token


<embed src='/assets/images/eb_postman.png' width='100%' height='100%' style='display: block; margin: 0 auto'>

N.B Eventbrite handles pagination differently than SmartSurvey. As per above the result starts with a “pagination” object with pages count information and a “continuation” code. To get the next page, send the same request again, but with an extra ```“continuation``` parameter set (in my case ```eyJwYWdlIjogMn0```).


### Eventbrite API endpoints

There are many endpoints with Eventbrite API. Here are two:

**1. https://www.eventbriteapi.com/v3/organizations/0123456789/events?expand=organizer,venue** 

This returns all events that an organisation has ever created (the number 0123456789 for instance would be the organisation ID):


**2. https://www.eventbriteapi.com/v3/organizations/1234561011/events?expand=organizer,venue** 

The second enpoint above calls and returns all tickets attached to an event with additional information about attendees - as shown in Postman below:


<embed src='/assets/images/eb2_postman.png' width='100%' height='100%' style='display: block; margin: 0 auto'>

Pagination information shown and then a list of all the orders for that event.
