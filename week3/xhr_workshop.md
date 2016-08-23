# Workshops

# XHR Workshop

# How do you use XHR to query APIs?

XHR stands for XML Http Request. This is actually an object (built-in for all modern browsers) that can be accessed by its name: XMLHttpRequest. It has a whole array of methods available to it in order to interact in different ways with a server. Note the odd capitalisation (XML is all caps, but only the 'H' of Http is).

Here is a simple example of how you can make an XML request:

```javascript
var myRequest = new XMLHttpRequest();
myRequest.onreadystatechange = function() {
    if (myRequest.readyState == 4 && myRequest.status == 200) {
      document.getElementById("demo").innerHTML =
      myRequest.responseText;
    }
};
myRequest.open("GET", "xmlhttp_info.txt", true);
myRequest.send();
```

[You can see it in action here.](http://www.w3schools.com/ajax/tryit.asp?filename=tryajax_first)

Read through the code to get an impression of the structure and what's going on. Then read this step-by-step walk-through of the different parts:

1. `var myRequest = new XMLHttpRequest();` --- this creates a new instance of the XHR object, which you can then use to query a server or file of your choice.

2. `myRequest.onreadystatechange = function() {...}` --- this method of the XHR object enables you to store a function (after the '=') which will be called automatically each time the `readyState` property of the `myRequest` object changes. [More here.](http://www.w3schools.com/ajax/ajax_xmlhttprequest_onreadystatechange.asp)

3. `if(myRequest.readyState == 4 && myRequest.status == 200){...}` --- every time the `readyState` property changes, the function will check if these two functions are met:
 1. `myRequest.readyState == 4` --- the `readyState` property changes from 0 to 4 as the request is processed. 0 means the request is not initialised, while 4 means the request is finished and the response is ready. However, the response might be that the request hasn't found what it was meant to, which is why we also need:
 2. `myRequest.status = 200` --- this property is only valid after the send method returns successfully. It will return a 3-digit status code starting with 1, 2, 3, 4, or 5, indicating what the result of your request was. The code `200` means 'OK', while `404` is notoriously the code for 'Not found'. [Full list here, under 'Return Values'.](https://msdn.microsoft.com/en-us/library/ms767625)
4. `document.getElementById("demo").innerHTML =
myRequest.responseText;` --- this is the code that will run if the request is successful. It generally does something with the response text (which is accessed with `myRequest.responseText`)
5. `myRequest.open("GET", "xmlhttp_info.txt", true);` --- the [open method](https://msdn.microsoft.com/en-us/library/ms757849) is important. Here it takes 3 parameters:
 1. *method*: The HTTP method to use (GET, POST, PUT, DELETE, PATCH, etc)
 2. *url*: The requested URL (in this case a local file path: "xmlhttp_info.txt") - in many cases this will be the URL of the server you are querying.
 3. *async* (optional): whether the call should be asynchronous or not. `false` means it waits for a response from the server before continuing execution of the code. The default value is `true`, which allows you to execute other scripts while waiting for the response. This is generally preferable.
6. `myRequest.send();` --- this method sends the request to the server. Use this after setting up the XHR with the .open() method. If you are GETting, it takes no parameter, but if you are POSTing, it may take a parameter of the string you wish to post.

# Resources
* [W3Schools Guide to AJAX](http://www.w3schools.com/ajax/default.asp) --- the whole thing is useful, but in particular:
    * [W3Schools Guide to the XMLHttpRequest Object](http://www.w3schools.com/ajax/ajax_xmlhttprequest_create.asp)
    * [W3Schools Guide to Sending a Request to a Server](http://www.w3schools.com/ajax/ajax_xmlhttprequest_send.asp)
* [You don't need jQuery to make Ajax requests!](http://blog.garstasio.com/you-dont-need-jquery/ajax/)


# TfL walkthrough with Postman

## Installing Postman
Go to Chrome store and install Postman 
[Postman on Chrome Store](https://chrome.google.com/webstore/search/postman%20api?hl=en-US)

## What
Postman is a tool which you can use to create and send HTTP requests. You can also use it to write tests to help you validate information about a response.

Some features of using Postman to create requests: 
1. make more detailed requests
2. select request methods from dropdown
3. add a body to your request
4. add headers

## Interface

The main area of the Postman interface is the 'request builder' section. Here you can create and send all different types of requests.

Using the request builder:
- Add the url you want to make a request to
- Click the Params button to add any parameters to your request. Parameters are variable parts of a resource. The documentation of the API you're using should tell you which params are available for each resource (if any). You can also use the params section for path variables (e.g. https://api.library.com/:entity/) More on this below.
- Use the HTTP method drop down to select your request method
- You can set headers and a body (if making a request that isn't a GET request) using the 'Header' and 'Body' tabs

## TfL API

Go to https://api.tfl.gov.uk/

### Anonymous requests:

You can make GET requests to the tfl api without registering for an app_id and app_key. However, usage is limited.

### Using path variables

Have a look at the docs and choose an endpoint to make an anonymous request via postman. e.g. https://api.tfl.gov.uk/Line/{id}

The {id} part of the url is a path variable which you can set in postman like this:
- Enter the url https://api.tfl.gov.uk/Line/:id/ in Postman
- Click the params button. You'll see the id has been added as a parameter
- Set the value of id to a tube line name e.g. victoria (you can add multiple line names by separating each one with a comma)
- Make sure your method is set to GET and click 'Send'
- The response data is displayed in the body tab. While headers are shown in the Header tab.

Let's look at the Arrival information of Victoria line trains.

Make a request to the following url via Postman:
https://api.tfl.gov.uk/Line/victoria/Arrivals
This gives information on a train's destination and when it is expected to arrive at a particular station.

### Setting request params

You can retrieve Arrival information on a particular station using the following endpoint:
/Line/{ids}/Arrivals?stopPointId={stopPointId}

If you inspect the docs you'll see that the stopPointId corresponds to naptanId in our last request. Copy a naptanId from your previous request and add it as a param in our new endpoint e.g.:
- if my naptanId is 940GZZLUWWL, click the params button and set key as 'naptanId' and value as '940GZZLUWWL'
- click Send

### Registering for an app_key and app_id

For a higher rate limit register for:
 - app id (this should be sent with every request)
 - app key (TfL uses this to authenticate requests)
 
Register here: https://api-portal.tfl.gov.uk/signup

Make a request to the TfL API in postman and add your app_id and app_key as params.

## Tests

Postman also has a tab that let's you test the response you get from a server. Tests are written in JS and you have access to a 'tests' object.

Example of a test:
tests[“Body contains user_id”] = responseBody.has(“user_id”) 
Try a similar test with the data we got from the TfL API.

There is a list of example tests you can try out on the RHS of the Tests section.

## POST requests
Making a POST request:
 - POST requests require you to put data in the body of your request. You can't do this via the browser. Postman gives you an environment for making POST requests and the option to add Authorisation information.
- With Web APIs you need to get authentication and authorisation in order to make a POST request. These are topics that will be covered in a later week so don't worry about POST requests for now.