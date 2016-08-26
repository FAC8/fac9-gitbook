# Week 4
This week you will be introduced to *Node*, *Node Package Manager*, Node servers, and you will end building your own server and your own API.

## What is node?

At the beginning, [Netscape](https://en.wikipedia.org/wiki/Netscape) created JavaScript as feature of its browser to make websites more interactive. It will make them able to run some small scripts and animations on websites when they where almost static content. I don't want to bother you with historical stuff, but if you want to know more about the JavaScript beginnings, I recommend you to read [this](https://en.wikipedia.org/wiki/JavaScript#Beginnings_at_Netscape) wikipedia article.

In mid-2000s the popularity of JavaScript start growing with web applications like Gmail. And after google open sourced [Chromium](https://en.wikipedia.org/wiki/Chromium_%28web_browser%29) people started to think about taking its JavaScript engine [V8](https://en.wikipedia.org/wiki/V8_%28JavaScript_engine%29) to use it also outside of the browser.

So even though some people tend to think that node is a new language, it's not, it is only a new environment out of the browser to run JavaScript. That enviroment don't have access to the window, or to the [DOM](https://en.wikipedia.org/wiki/Document_Object_Model) as you have in your browser JavaScript. On the other hand, Node enviroment let you access to the file system, network or other staff that other languages like php gives you by default in its standard library. All this new cool things will allow us to use JavaScript to build web servers (backends), command line applications.

> If at this point you still not seeing clear what's the difference between frontend and backend, you should read [this](https://en.wikipedia.org/wiki/Front_and_back_ends). In a few words, the frontend is everything you see in your browser, and the backend is the application server you are running in your server.

## Node package manager

Node package manager \(npm from now\) is a tool for managing packages that comes with Node. It allows us to install tools, packages as depencies of our projects, and also publish our own packages.

npm commands

* `npm init`: Initialize a package and create a `package.json` with the definition of that package. 

* `npm search MODULE_NAME`: Search a module in the npm registry.

* `npm install MODULE_NAME`: Install MODULE\_NAME locally.

  * `npm install -g MODULE_NAME`: install MODULE\_NAME globally.

  * `npm install --save MODULE_NAME`: install MODULE\_NAME locally and add it as a dependency in the package.json.

  * `npm install --save-dev MODULE_NAME`: install MODULE\_NAME locally and add it as a development devependency in the package.json.

## Node core modules
We are going to work mainly with 2 Node core modules, **http** and **fs**, but below we are going to show and describe a few more:

* [**http**](https://nodejs.org/api/http.html#http_http): This module provide an interface for creating servers and clients supporting the [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) protocol. We be mainly working with the function [`createServer`](https://nodejs.org/api/http.html#http_http_createserver_requestlistener) of that module, but you are free to learn it more deeply.   

* [**fs**](https://nodejs.org/api/fs.html#fs_file_system)

* **path**

* **url**

* **querystring**

* **util**

> Create readmes about those modules? at least http and fs?

