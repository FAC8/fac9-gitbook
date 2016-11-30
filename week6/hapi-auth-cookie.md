# Hapi-auth-cookie: quick guide

## Set up

``` javascript
var Hapi = require('hapi')  
var CookieAuth = require('hapi-auth-cookie')

var server = new Hapi.Server()

server.register(CookieAuth, function (err) {

  server.auth.strategy('base', 'cookie', options) 

  server.start(function (err) {
    console.log('info', 'Server running at: ' + server.info.uri)
  })
})
```

###### What is a strategy?

A strategy is a configured instance of a *scheme*.

###### OK so what's a scheme?

It's a type of authentication that you define. You might use different schemes to authenticate administrators and users, for example. In this case we are creating a scheme called 'base' - we do not need multiple schemes. We could use any name for our scheme, but we will need to use the name we choose to refer to our scheme later.

## Login a user

Logging someone in is called creating a session. We will create a session by creating a cookie. That's why the second argument to `strategy` is `'cookie'`.

```javascript
server.route({  
  method: 'POST',
  path: '/login',
  config: {
    handler: function (request, reply) {
      var username = request.payload.username
      var password = request.payload.password

      // Check username and password details against database.
      // Return an object with data uniquely identifying user.
      // Lets call this object user.
      
      if (user) {
        request.cookieAuth.set(user);
        reply('logged in')
      }
    }
  }
})
```

## Add auth to your routes

We can simply block a route for users without a set cookie:

```javascript
server.route({  
  method: 'GET',
  path: '/some-route',
  config: {
    auth: {
      strategy: 'base' 
      },
    handler: function (request, reply) {
      return reply('you’re authenticated :)')
    }
  }
})
```

The plugin will check if a cookie has been set and if not, block access, intercepting before the handler is called.

Or we can allow access to the route and handle the session checking in the handler:

```javascript
server.route({  
  method: 'GET',
  path: '/some-route',
  config: {
    auth: {
      mode: 'try',
      strategy: 'base' 
      },
    handler: function (request, reply) {
      if (request.auth.isAuthenticated) {
        return reply('you’re authenticated :)')
      }
    }
  }
})
```

## Access details of the logged in user

Easy: `request.auth.credentials`. We get back whatever we passed to `set`.

## Logout (end session)

Also easy: `request.cookieAuth.clear()`. No more cookie!

## Strategy config

What about the `options` we passed to `strategy`? Here's an example:

``` javascript
options = {
    password: 'm!*"2/),p4:xDs%KEgVr7;e#85Ah^WYC',
    cookie: 'cookie-name',
    isSecure: false,
    ttl: 24 * 60 * 60 * 1000
  })
```

Notes:
 - Password should be at least 32 chars. The plugin will encrypt and decrypt your cookie using it.
 - Cookie name can be anything.
 - isSecure, if `true`, will prevent the cookie being sent on insecure connections. Hapi seems to consider localhost as insecure, so set it to `false` for development and `true` for production (assuming you are hosting on https).
 - ttl sets when the session will automatically expire in milliseconds after creation.

There are lots more options you can set. Check the docs for the plugin.
