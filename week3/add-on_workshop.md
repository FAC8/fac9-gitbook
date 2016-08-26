# Add-on workshop


### workshop by an alumni or FAC tutors (TBC)


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
