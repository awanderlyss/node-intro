[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Introduction to Node JS

## Objectives

By the end of this, developers should be able to:

-   Understand what is Node.JS
-   Vizualize the difference between Node and other backend environments, such as Sinatra.
-   Set up a basic server
-   Create a GET request with vanilla Node.
-   Install and include node modules


## What is Node?

Node is a JavaScript runtime environment that is event driven and uses a non-blocking input/output model.

Most server-side environments will enter something called an event loop. But in most cases, when an event is triggered, the code will not move on to any other event until the first one has been completed. This is where the non-blocking feature of node comes in handy. Node will set aside the event if it is not done, allowing other events to be triggered. When the event is complete it will fire the code right away.

***For example:***

Say I am using a home budget web application, I have a lot of transactions that I have to load up, so while I am waiting for the server to respond to list all those transactions, I can use a server-side calculator to calculate my taxes for the year on the same page.

If some of this language is unfamiliar, there is a full article on [Blocking vs Non-Blocking](https://github.com/nodejs/node/blob/master/doc/topics/blocking-vs-non-blocking.md).

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

In this case I am goind to use a random number website [www.random.org](www.random.org) to get some dummy data for this example.

```js
let options = {
   host: 'www.random.org',
   path: '/integers/?num=1&min=1&max=10&col=1&base=10&format=plain&rnd=new',
   method: 'GET'
};

let callback = (response) => {
  //response is the parameter where we will recieve the data
};

let request = http.request(options, callback);
```

Now, when we recieve data over the server, it does not come in one complete chuck of data. Information received comes through in bits and pieces.

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
   host: 'www.random.org',
   path: '/integers/?num=1&min=1&max=10&col=1&base=10&format=plain&rnd=new',
   method: 'GET'
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
