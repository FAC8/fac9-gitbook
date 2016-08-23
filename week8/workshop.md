# Workshop
In this workshop we will be implementing an OAuth workflow from scratch using the Github API. The full OAuth guide for github can be found [here](https://developer.github.com/v3/oauth/).

Pair up and try to complete each step in turn.

#### Step 1 -- Setup a basic Web server
We need a server running before we can do anything.
* Create a new npm project
* Install `hapi` and `inert`
* Create a simple Hapi server that serves up a 'Hello World' `html` file at `/`
* Create a `config.env` file for your project and store your server address in a variable called `BASE_URL`

#### Step 2 -- Write a request function
We'll need to send an `https` request. Write a function to make it easier for us.
* Write a function called `request` that can send `GET` and `POST` requests using the `https` native module
* Your function should have the following signature
```javascript
function request(<Object> options, <Function> callback)
```
* The `options` object here should correspond directly to the options object that is passed to the request method of the `https` module. The `callback` function you pass in should be executed after a response is receieved.
* Hint: remember you need to chunk your response! Remember the standard node callback pattern of `callback(error, result)`.

#### Step 3 -- Register your app
Github needs to know about your app before it will let you authenticate users with it.
* Go to Github profile settings > OAuth applications > Developer applications > Register new application
* Register your app. Call it what you like
* In the `homepage url` field type your `BASE_URL` (e.g. `http://localhost:3000`)
* In the `authorization callback url` field, type your `BASE_URL` + `/welcome` (e.g. `http://localhost:3000/welcome`)
* Add two new variables to your `config.env`: `GITHUB_CLIENT_ID` and `GITHUB_CLIENT_SECRET`, taken from your app page.

#### Step 4 -- Create your login route
This is the url on our server which will begin the OAuth workflow.
* In your Hapi server, create a route `GET /login` which redirects the user to `https://github.com/login/oauth/authorize` along with two query parameters:
  * `client_id`
  * `redirect_uri`
* Hint: use the `querystring` native module to generate your query string. What is `reply.redirect`?

#### Step 5 -- Create your redirect route
We provided a redirect URI to Github to which it will send the user after they have logged in and granted our app permission. Now we should create that route on our server to retrieve the access token that we need to access the Github API on behalf of the user.
* In your Hapi server, create a route `GET /welcome` which sends a request to 
```
POST https://github.com/login/oauth/access_token
```
* The body of the request needs the following fields:
  * `client_id`
  * `client_secret`
  * `code`
* For now, simply reply with the body of the response.
* Hint: the `code` will be sent to you at the redirect URI as a query parameter (e.g. `/welcome?code=foo`. How do you access query parameters using the `request` object?

#### [Bonus] Step 6 -- Store your access token
If we get this far, we can now use our access token to make requests to the Github API on behalf of the authenticated user. But before we can do that we need a way to store the token so we can access it in other routes.

Typically, this is done either in a database, or in a secure cookie (e.g. JWT). However, this is overkill for a simple tutorial, so for now, just store it in the server app container. That is, at the end of your welcome route:
```javascript
server.app.access_token = access_token;
```
The app container will persist as long as your server is running. Check the `Hapi` docs for more information about this.

#### [Bonus] Step 7 -- Use your access token
Now create another route, with any name, that uses your access token to send a request to the Github API. Explore the Github API. If you're stuck for ideas, try to follow a user using an API request. You may need to re-authenticate the using the `user:follow` scope.