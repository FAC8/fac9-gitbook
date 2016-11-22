# Learning Outcomes

This week, you'll be learning the basics of the node framework Hapi:

### Core Learning Outcomes

+ Set up a Hapi Server (get it listening on a `port` of your choice)
+ Set up some routes using `server.route([....])`
+ Get data out of the `request` params and payload
+ Set up a route with a dynamic url (i.e. one route that can handle a number of different requests)
+ Register Plugins using the `server.register([....], cb)` method
+ Serve static files (like css or js files) using the `Inert` plugin
+ Serve html templates using `Handlebars` and Hapi's `Vision` plugin
+ Validate a user's input using the `Joi` plugin
+ Set up a basic user login with the `Hapi Auth Basic` plugin
+ Test all of these using `tape` (Hapi has `shot` built in so it's super nice to test!)

If you can do all of these, congratulations!!

### Bonus Learning Outcomes

+ Understand and use Handlebars partials, layouts and helpers
+ Organise a 'feature' of your app into a Hapi plugin
