# Project

Your project this week is to build a simple hapi app using test driven development that queries at least two APIs on the backend and uses the retrieved data to populate a handlebars template that will use server-side rendering to be displayed on the front-end.

Here is a list of [public APIs](https://github.com/toddmotto/public-apis) you might consider. Please bare in mind if the API requires the user to log-in to authenticate and give you permission to use their data, this is called oAuth and will be covered in week 8. Do not use any APIs that require oAuth!

What you choose to build with this data and how you choose to display it is up to you. But I would suggest you

* In the planning phases, have a think about user stories. Who are you building this for? What problem are you trying to solve? You might find the notes on Nelson's talk in your [notes](https://github.com/FAC9/notes/tree/master/week5/nelson-workshop) repo useful.
* Try to build this tdd as far as you are able to using the techniques and `server.inject` method that Francesco showed you.
* Aim for as high test-coverage as possible.
* Try to use basic ES6 syntax in this project:
1. `const` for all variables whose values will never be re-assigned.
2. `let` for all variables whose values will be re-assigned.
3. `(arg1, arg2) => {}` arrow functions whenever you need callbacks.
4. `template ${literals}` whenever you use strings that require concatenation: i.e. 'string 1 ' + 'string 2'.