[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Introduction to Node JS

## Objectives

By the end of this, developers should be able to:

-   Understand what is Node.JS
-   Vizualize the difference between Node and other backend environments, such as Sinatra.
-   Set up a basic server
-   Create a GET request with vanilla Node.
-   Install and include node modules using ES6 and ES5


## What is Node?

Node is a JavaScript runtime environment that is event driven and uses a non-blocking input/output model.

Most server-side environments will enter something called an event loop. But in most cases, when an event is triggered, the code will not move on to any other event until the first one has been completed. This is where the non-blocking feature of node comes in handy. Node will set aside the event if it is not done, allowing other events to be triggered. When the event is complete it will fire the code right away.

***For example:***

Say I am using a home budget web application, I have a lot of transactions that I have to load up, so while I am waiting for the server to respond to list all those transactions, I can use a server-side calculator to calculate my taxes for the year on the same page.

Simply put, Node is an asychronous server-side environment to write API and server-side web applications.

Just like Ruby has Rails and Sinatra, JavaScript has Node.

***What are some aspects of rails/sinatra that you learned?***

Just like in Rails and Sinatra, we will be running servers, create RESTful routing, interact with a database, including external code packages, and using a MVC design patterns.

## I DO - Node in the Terminal.

***Just watch me for now***

Another thing Node can be used for is a REPL for JavaScript in the terminal.

If you remember when we learned JavaScript, we would use our console in Chrome in order to test our code. We can do the same with Node in our terminal.

We can launch the REPL environment by simple trying in the command:

```bash
$ node
```

Which should look similar to our `rails c` or ` irb` environments from ruby. You should see something like this:

```bash
~ (master)$ node
> 
```

From here we should be able to type out plain JavaScript. 

We can type out operators, set variables, creation functions, call functions, etc.

```bash
~ (master)$ node
> 1+1
2
> var name = "Eric"
undefined
> name
'Eric'
> function sayName(name){
... console.log(name);
... }
undefined
> sayName(name)
Eric
undefined
> 
```

*Note - where you see the undefined here, this would be a returned value from a function.

If I have a JavaScript file, I can run it in the terminal as well.

I am going to create a new JavaScript file called `app.js` and add the function below:

```js
(function sayName(){
  console.log("Eric Stermer");
}());
```

Then run it by typing this command in the terminal:

```bash
$ node app.js
```

Which should output `> Eric Stermer` because the function we created was an IIFE (immediately invoked function expression).
