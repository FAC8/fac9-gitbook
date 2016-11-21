# Project

Your project this week is to build a simple hapi app using test driven development that queries at least two APIs on the backend and uses the retrieved data to populate a handlebars template that will use server-side rendering to be displayed on the front-end.

Here is a list of [public APIs](https://github.com/toddmotto/public-apis) you might consider. Please bare in mind if the API requires the user to log-in to authenticate and give you permission to use their data, this is called oAuth and will be covered in week 8. *Do not use any APIs that require oAuth!*

What you choose to build with this data and how you choose to display it is up to you. But I would suggest you

* In the planning phases, have a think about user stories. Who are you building this for? What problem are you trying to solve? You might find the notes on Nelson's talk in your [notes](https://github.com/FAC9/notes/tree/master/week5/nelson-workshop) repo useful.
* Try to build this tdd as far as you are able to using the techniques and `server.inject` method that Francesco showed you.
* Aim for as high test-coverage as possible, on front-end and back-end.
* Host the project on heroku.

Try to use basic ES6 syntax in this project:
* `const` for all variables whose values will never be re-assigned.
* `let` for all variables whose values will be re-assigned.
* `(arg1, arg2) => {}` arrow functions whenever you use callbacks.
* `template ${literals}` whenever you use strings that require concatenation: i.e. 'string 1 ' + 'string 2'.

The aim of this project is to integrate the knowledge you've been acquiring over the last few weeks not to stretch you too far. I'd rather you integrated past knowledge like modularisation, continuous integration, and hosting, than go into hapi's validation, authentication, and session management capabilities.

Please bare in mind these latter topics become especially relevant once you have a database and were introduced on readme day to give you basic familiarity before going into next week, and to get familiar with hapi's capabilities and documentation.