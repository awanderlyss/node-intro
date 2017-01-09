[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Introduction to Node JS

## Objectives

By the end of this, developers should be able to:

-   Understand what is Node.JS and why we would build apps in Node.
-   Recognize the benefits of writing web applications using Node.
-   Compare and contrast JavaScript in the client to JavaScript in Node.
-   Compare and contrast the Node library and web frameworks such as RoR and Sinatra.
-   Navigate the Node REPL and deploy simple node apps.
-   Set up a basic web server.
-   Create a GET request with vanilla Node.


## What is Node?

Node is a JavaScript runtime environment built with Chrome's V8 engine that is event driven and uses a non-blocking input/output model. It is available as an open source library, and designed to build scalable network apps, chosen for it's ability to create parallel applications.

Most server-side environments will enter something called an event loop. But in most cases, when an event is triggered, the code will not move on to any other event until the first one has been completed. This is where the non-blocking feature of node comes in handy. Node will set aside the event if it is not done, allowing other events to be triggered. When the event is complete it will fire the code right away.

***For example:***

Say I am using a home budget web application, I have a lot of transactions that I have to load up, so while I am waiting for the server to respond to list all those transactions, I can use a server-side calculator to calculate my taxes for the year on the same page.

If some of this language is unfamiliar, there is a full article on [Blocking vs Non-Blocking](https://github.com/nodejs/node/blob/master/doc/topics/blocking-vs-non-blocking.md).

Simply put, Node is an asychronous server-side environment to write API and server-side web applications.

Just like Ruby has Rails and Sinatra, JavaScript has Node.

***What are some aspects of rails/sinatra that you learned?***

Just like in Rails and Sinatra, we will be running servers, create RESTful routing, interact with a database, including external code packages, and using a MVC design patterns.

Though Node is used to write powerful web server applications, it is not a framework like Rails or Sinatra. It is more comparable to Ruby in that it is an interpreted language on your local machine.

If you remember, JavaScript was only written in the Client. Now with Node, we can write JavaScript on our local machine.

This is different from a Web Framework because it does not have the full functionality of creating models, generating partial views, and seperating out concerns with routing. Node does have a framework written for it called 'Express' which we will get into after this lesson.

## Why use Node over other backend languages?

#### Node is JavaScript

Ultimately, Node is simply JavaScript. This aspect of node breaks down the barrier between frontend web developers and backend developers. People who are familiar with just JavaScript can learn to write server side code easier which creates greater continuity from front to the back, meaning greater productivity.

For example:
PayPal measured a 2x increase in developer productivity, where it took half the number of developers to deliver an application when compared to Java, and it was delivered in less time.

#### Performance due to asynchronousity

Because of the non-blocking nature of Node, it can handle multiple requests at the same time.

Walmart took advantage of this and switch over to running their mobile traffic through Node.js in 2013 for Black Friday.

For such a busy day of the year to process orders online, Walmart's servers didn’t go over 1% CPU utilisation and the team did a deploy with 200,000,000 users online.

#### Adaptability and Easy Maintenance

Unlike Ruby on Rails, servers written in Node are not so opinionated in their development. This makes for greater adaptability. Incase the application is not designed for a specific purpose, it can be mutable.

## I DO - Node in the Terminal.

***Just watch me for now***

Since Node is a runtime environment for JavaScript on your local machine, it has a REPL environment.

If you remember when we learned JavaScript initially, we would use our console in Chrome in order to test our code. We can do the same with Node in our terminal.

We can launch the REPL environment by simple trying in the command:

```bash
$ node
```

Which should look similar to our `rails c` or ` irb` environments from ruby. You should see something like this:

```bash
~ $ node
> 
```

From here we should be able to type out plain JavaScript. 

We can type out operators, set variables, creation functions, call functions, etc.

```bash
~ $ node
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

With Node you have access to a lot of the built in methods you saw using JavaScript in the client. Instead of being inherited from the `Window` object like we see in the client, they inherit from the `Global` object. Other than that, there is very few differences between Node and the Client.

Next, if I have a JavaScript file, I can run it in the terminal as well.

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

Which should output `Eric Stermer` because the function we created was an IIFE (immediately invoked function expression).

## YOU DO - Play Around With Node REPL (5 Mins)

### Break (10 mins)

## Build A Server - 'Hello World'

Now that we have some experience running Node on our machine, lets start up our first web server using Node.

To get started we need to require the `http` interface which provides the ability to create our server and RESTful routing.

```js
const http = require('http');
```

Then lets define the local host name and the port number we want the server to run on.

```js
const hostname = '127.0.0.1'; // this is our localhost
const port = 3000;
```

Now that we have `http` added to our file, we can create our server with a method available to us through `http`.

This method call `createServer` takes in one argument which is function callback whose parameters are the servers `request` and the servers `response` which we will shorten up to `req` and `res`.

```js
const server = http.createServer((req, res) => {

});
```

`request` is an object that contains the information that is coming in as a string.
`response` is an object that contains methods for what you want to do with the data once you have it and are done with it.

So when our server is first pinged, lets give it some information back using our `response` object.

```js
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});
```

With the code above we are sending a status code of `200` meaning everything is good. Also we set the implicit header type to `text/plain` which is the kind of content that we will receive from requests unless otherwise specified. And lastly, with the `end` method we tell the route that we are done and to send something to the client, in this case we are just sending text to be rendered saying `Hello World`.

The last thing we need to get our server to work, is we need our server to enter the event loop and to listen on the path that contains the hostname and port number.

```js
server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

You will notice a `console.log` in the callback function. This will output to our console/terminal for us to confirm that our server is infact working. It is only visual organization and not required.

We are done creating our server, now we can run it.

Like we said before, we run js files with node using the `node` command in our terminal. So lets to that:

```bash
$ node server.js
```

which should get us something like this:

```bash
~ $ node server.js 
Server running at http://127.0.0.1:3000/
```

If we copy and paste the path we see in our terminal where our server is listening on and paste it to our address bar in chrome we should see `Hello World` displayed.

Now if we wanted to show `I Like Pizza` underneath our `Hello World` in the browser we could simple add it to our `res.end()` methodlike this:

```js
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n I Like Pizza');
});
```

Which will now show that `I Like Pizza` bellow the `Hello World`.

***OOPS***

When we refreshed our page it doesn't show that we like pizza yet. Why is that? This is because we need to refresh our browser once we have saved changes to our server file. 

So go ahead and `ctrl + c` to cancel our server and rerun the command `node server.js`.

Now if we refresh the browser we will see that `I Like Pizza` is now showing.

***Now That Is Annoying***

Having to restart your server after every saved change is not fun. So like `sintra/reloader` for Sinatra to help automatically reload the server when changes are saved, Node has something called `nodemon` which is a node package that does the same thing.

To download it run the command:

```bash
$ npm install nodemon -g
```

This will globally install nodemon to your computer allowing you to use it on any project without having to redownload it.

Then to run our server you just run:

```bash
$ nodemon server.js
```

### Break (5 mins)

## REST For Node

Just like any other server, Node uses the RESTful routing convention to speak to clients and other servers. The most common of these is the 'GET' method, which is simply a method to read data from a source.

Our RESTful methods in Node are a property of `http`.

So to write a 'GET' method, we will create an instance of our request with a variable, setting it to the `http.request()`.

```js
var request = http.request();
```

HTTP requests takes in two arguements, an [options](https://nodejs.org/dist/latest-v6.x/docs/api/http.html#http_http_request_options_callback) object that contains information about the source of your data such as the path and host, and a callback function where we will manipulate the data when it is received.

In this case I am going to use a starwars search  website [www.swapi.co](www.swapi.co) to get get information about Luke Skywalker.

```js
let options = {
  method: "GET",
  hostname: "swapi.co",
  path: "/api/people/1/",
};

let callback = (response) => {
  //response is the parameter where we will recieve the data
};

let request = http.request(options, callback);
```

Now, when we recieve data over the server, it does not come in one complete chunk of data. Information received comes through in bits and pieces.

So in our callback function, there is a method in our response that is somewhat like an event listener that we have seen in JavaScript DOM manipulation. 

We use the `on` method to listen for `data` and concatenate the data into a single string. Remember also that data is sent through the internet as strings and is the only way data can be sent and received.

So, in our callback lets create a variable first that will represent our data and set it to an empty string:

```js
let callback = (response) => {
  let data = "";
};
```

Then lets use `response.on()` to listen for `data` and pass a callback function that adds the chuck of data to our data variable.

```js
let callback = (response) => {
  let data = "";
  
  response.on('data', (chunk) => {
    data += chunk;
  });
};
```

Now everytime a peice of data is received by our request method, it will add the piece to the whole. 

Once this process is complete, we have to manually tell out request method what to do onces all the information is received. In this case we just want to log the data to our terminal/console. We do this with another event listener that listens for when all the data is received, allowing us to fire a callback which is where we will `console.log` our data.

```js
let callback = (response) => {
  let data = "";
  
  response.on('data', (chunk) => {
    data += chunk;
  });
  
  response.on('end', () => {
    console.log(data);
  });
};
```

We are not quite done with our request.

One last thing we need to do is stop our request from asking for information from the source manually. This is done with another `http` method called `end`. 

So our entire 'GET' request should look like this:

```js
// Options is an object to include information regardnig the 5 W's of the data we want
let options = {
  method: "GET",
  hostname: "swapi.co",
  path: "/api/people/1/",
};

// The callback function allows us to gather and manipulate the data we receive
let callback = (response) => {
  let data = "";
  
  // Data comes in pieces so we listen for those pieces and add them together
  response.on('data', (chunk) => {
    data += chunk;
  });
  
  // The response listens for when the all the data comes through to then do something with the data
  response.on('end', () => {
    console.log(data);
  });
};

// This variable opens up the request 
let request = http.request(options, callback);

// This end method closes the request
request.end();
```

Checking our server we should see this:

```bash
Here is information about Luke: {"name":"Luke Skywalker","height":"172","mass":"77","hair_color":"blond","skin_color":"fair","eye_color":"blue","birth_year":"19BBY","gender":"male","homeworld":"http://swapi.co/api/planets/1/","films":["http://swapi.co/api/films/6/","http://swapi.co/api/films/3/","http://swapi.co/api/films/2/","http://swapi.co/api/films/1/","http://swapi.co/api/films/7/"],"species":["http://swapi.co/api/species/1/"],"vehicles":["http://swapi.co/api/vehicles/14/","http://swapi.co/api/vehicles/30/"],"starships":["http://swapi.co/api/starships/12/","http://swapi.co/api/starships/22/"],"created":"2014-12-09T13:50:51.644000Z","edited":"2014-12-20T21:17:56.891000Z","url":"http://swapi.co/api/people/1/"}
```

## Summary

Node is chosen for it's asynchronous capabilities. Because of this, companies like Walmart were able to handle huge numbers in traffic to their online shopping application without risking speed!

Vanilla Node is rarely used on its own. This lesson was simply to introduce to using JavaScript as a web server language.

We will cover a web framework called 'Express' which is used on top of Node to make life easier when it comes to writing a web server in JavaScript.

Some summary questions:

- What language does Node interpret?
- If Node a Framework or a Library?
- On what engine is Node built on?
- Name 3 reasons why we would use Node rather than another Server side language?


