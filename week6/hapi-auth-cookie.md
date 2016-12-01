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

It's the type, i.e. the *manner*, of authentication. Hapi-auth-cookie creates a scheme called 'cookie', which we reference when creating our strategy (the second argument of `strategy`). You have also seen a scheme called 'basic', which provides a different kind of authentication.

Here we configure our scheme with `options` and give our *strategy* (configured scheme) the name 'base'. We could use any name for our strategy, but we will need to use the name we choose to refer to it later.

###### Why distinguish between scheme and strategy?

We might want to use more than one strategy of the same scheme. For example, if we have two different classes of users (ordinary users and administrators) defining two strategies will allow us to set different permissions on routes more easily. In this case we are creating one strategy called 'base' - we do not need any more.

## Login a user

Logging someone in is called creating a session. We will create a session by creating a cookie using the `set` method of the `cookieAuth` object which (by default) the plugin adds to the request object.

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

Now we can check whether a cookie has been set by ocnfiguring the `auth` object of a route. We can simply block a route for users without a set cookie:

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
 - Password should be at least 32 chars. The plugin will encrypt and decrypt your cookie using it. In real life this should not be written into your code.
 - Cookie name can be anything.
 - isSecure, if `true`, will prevent the cookie being sent on insecure connections. Hapi seems to consider localhost as insecure, so set it to `false` for development and `true` for production (assuming you are hosting on https).
 - ttl sets when the session will automatically expire in milliseconds after creation.

There are lots more options you can set. If you want to define more than one strategy, you will need to make use of the `requestDecoratorName` option, for example. Check the docs for the plugin.

## Set defaults

You have the option of passing a `mode` argument to `strategy` in this position:

```javascript
server.auth.strategy(name, scheme, [mode], [options])
```

If you pass `true` or `'required'`, all routes will automatically be protected by the strategy. If you pass `'try'`, all routes will be protected, but with their `config.auth.mode` property set to try (see *Add auth to your routes* above).

## Gotcha!

Unlike the plugins you have used so far, hapi-cookie-auth loads asynchronously. That means anything you do to the server (`server.start`, `server.routes`) must be done in the `register` callback. This should make testing fun.


