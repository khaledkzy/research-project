 #  ![Node](https://heroku-elements.s3.amazonaws.com/buttons/uploaded_logos/000/002/550/icon/nodejs.png?1476395955) Request Life Cycle

**Request–response, or request–reply** is one of the basic methods computers use to communicate with each other, in which the first computer sends a request for some data and the second computer responds to the request.

The largest waste with current programming technologies comes from waiting for Req/RES to complete. 

When Node receives an HTTP request, it creates the req and res objects (which begin their life as instances of http.IncomingMessage and http.ServerResponse respectively). The intended purpose of those objects is that they live as long as the HTTP request does.

Because of Node's asynchronous nature, there could be multiple req and res objects at any given time, distinguished only by the scope in which they live. This may sound confusing, but in practice, you never have to worry about that: when you write your code, you write it as if you were always ever dealing with one HTTP request, and your framework (Express, for example), manages multiple requests.

**Request–response** is a message exchange pattern in which a requestor sends a request message to a replier system which receives and processes the request, ultimately returning a message in response. This is a simple, but powerful messaging pattern which allows two applications to have a two-way conversation with one another over a channel. This pattern is especially common in client–server architectures.

### Request-response lifecycle through a middleware is as follows:
Middleware functions are functions that have access to the request object (req), the response object (res), and the next middleware function in the application’s request-response cycle. The next middleware function is commonly denoted by a variable named next.

Middleware functions can perform the following tasks:

    Execute any code.
    Make changes to the request and the response objects.
    End the request-response cycle.
    Call the next middleware function in the stack.
    
```    
var app = express()

app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})
```


*If the current middleware function does not end the request-response cycle, it must call next() to pass control to the next middleware function. Otherwise, the request will be left hanging.*
    

![lifeCycle](https://vietcanho.files.wordpress.com/2016/06/middleware.png?w=1462)



### Amazone Web Service
![lifeCycle](https://image.slidesharecdn.com/5-160503081810/95/javascript-nodejs-development-on-amazon-web-services-33-638.jpg?cb=1462263535)





```
const http = require('http');

const server = http.createServer(function (req, res) {

    if (req.url === '/') { //check the URL of the current request

        console.log("New request to main page at " + Date())

        // set response header
        res.writeHead(200, { 'Content-Type': 'text/html' });

        // set response content    
        res.write('<html><body><h1>This is home Page.</h1></body></html>');
        res.write('<h2>The time is: ' + Date() + '</h2>');
        res.end();

    } else if (req.url === "/student") {

        console.log("New request to Student page at " + Date())

        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.write('<html><body><h1>This is student Page.</h1></body></html>');
        res.end();

    } else if (req.url === "/mentor") {

        console.log("New request to Mentor page at " + Date())

        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.write('<html><body><h1>This is mentor Page.</h1></body></html>');
        res.end();

    }

    else {
        res.end('<html><body><h2>Invalid Request at ' + Date() + '</h2></body></html>');
    }
});

server.listen(5000);

console.log('Node.js web server at port 5000 is running..')
```



![Req](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessageExample.png)
![Req](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessageExample.png)

Excersice

Here is an example of a simple “Hello World” Express application. The remainder of this article will define and add two middleware functions to the application: one called myLogger that prints a simple log message and another called requestTime that displays the timestamp of the HTTP request.
```
var express = require('express')
var app = express()

var myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}


app.get('/', function (req, res) {
  res.send('Hello World!')
})


app.use(myLogger)
app.listen(3000)
```

Every time the app receives a request, it prints the message “LOGGED” to the terminal.
The order of middleware loading is important: middleware functions that are loaded first are also executed first.
If myLogger is loaded after the route to the root path, the request never reaches it and the app doesn’t print “LOGGED”, because the route handler of the root path terminates the request-response cycle.
The middleware function myLogger simply prints a message, then passes on the request to the next middleware function in the stack by calling the next() function.

Famous Wbsite:
- Paypal
- Linkdin
- netflix
- Ebay




# research-project
 

## Preface
####  Developed by Ryan Dahl pada tahun 2009
####  Server Side Java Script
####  Built on Google’s V8 engine
####  An environment for developing high performance web services
####  Using event-driven, asynchronous I/O to minimize overhead and maximize scalability.
####  The goal is to provide an easy way to build scalable network servers
 
 Node is a server side JavaScript environment for developing web applications, application servers, any sort of network server or client, and general purpose programming.

 ![GitHub Logo](node.jpg)
 
 Node.js is the leading tool for creating server applications in JavaScript, the world’s most popular programming language. Offering the functionality of both a web server and an application server, Node.js is now considered a key tool for all kinds of microservices‑based development and delivery. 
 
 Node.js is single‑threaded and uses nonblocking I/O, allowing it to scale and support tens of thousands of concurrent operations. It shares these architectural characteristics
 

 
  Designed for high concurrency
  Without threads or newa processes
  Never blocks, not even for I/O
  Runs over the command line  
  Uses the CommonJS framework
  Making it a little closer to a real OO language
  
  ## Server-side JavaScript

  
Commonly JavaScript, jQuery was all still fronted stuff.
Node.js was JavaScript on the server.
It allows you to run JavaScript code in the backend, outside a browser.
Using runtime environment (Google’s V8 VM) and library (Node.js ships)


 ## What’s Node.js (cont’d)
 
  The Node model is very different from common application server platforms that scale using threads. The claim is that, because of the event-driven architecture, memory footprint is low, throughput is high, and the programming model is simpler.  
  The Node platform is in a phase of rapid growth, and many are seeing it as a compelling alternative to the traditional—Apache, PHP, Python, an so on—approach to building web applications. 

  Unlike in most other modern environments, a Node process doesn’t rely on multithreading to support concurrent execution of business logic, it’s based on an asynchronous I/O event-driven model. 
  
  
### What Can You Do  With Node ?
   
   It is a command line tool. You download a tarball, compile and install the source 
   
   It lets you run JavaScript programs by typing ‘node_my_apps.js” in your terminal
  
   It lets you Layered on top of the TCP library is a HTTP and HTTPS client/server 

  The JS executed by the V8 javascript engine (the ting that makes Google Chrome so fast)
Node provides a JavaScript API to access the network and file system.

## What can't Do With Node

  Node is a platform for writing JavaScript applications outside web browsers. This is not the JavaScript we are familiar with in web browsers. There is no DOM built into Node, nor any other browser capability. 
 
  One thing Node cannot do is desktop GUI applications. Today, there is no equivalent for Swing built into Node, nor is there a Node add-on GUI toolkit, nor can it be embedded in a web browser. 
  
  ## Why should use Node
  
   JavaScript is the popular language of the web
   
 “Global Object” as the main disadvantages of JavaScript, which can create an unruly chaos when mixing modules together
CommonJS module system from Node that make local variables are truly local

 Web applications spend most of their time doing I/O
Can implement the same programming language on client and server



## Node Potential Wins

The same programming staff can work on both ends of the wire

Code can be migrated between server and client more easily

Common data formats (JSON) between server and client

Common software tools for server and client

Common testing or quality reporting tools for server and client

When writing web applications, view templates can be used on both sides

Similar languaging between server and client teams

  
## Concurrency: The Event Loop
 
  Instead of threads Node uses an event loop with a stack
  Alleviates overhead of context switching
 
 
 
 ![GitHub Logo](node-queue.jpg)
 



 
 
 ## Event Loop Example 
 
   Request for “index.html” comes in
   Stack unwinds and ev_loop goes to sleep
   File loads from disk and is sent to the client


 ### Non Blocking I/O

  Servers do nothing but I/O
  Scripts waiting on I/O requests degrades performance
   To avoid blocking, Node makes use of the event driven nature of JS by attaching callbacks to I/O requests
  Scripts waiting on I/O waste no space because they get popped off the stack when their non-I/O related code finishes executing

 


### Consistancy 

  Use of JS on both the client and server-side should remove need to “context switch”
  Client-side JS makes heavy use of the DOM, no access to files/databases
  Server-side JS deals mostly in files/databases, no DOM
  JS Dom project for Node works for simple tasks, but not much else

 ![GitHub Logo](con.jpg)



Threads VS Event-driven

Events avoid concurrency as much as possible, threads embrace:
Easy to get started with events: no concurrency, no preemption, no synchronization, no deadlock
Use complicated techniques only for unusual cases
With threads, even the simplest application faces the full complexity.
Debugging easier with events:
Timing depedencies only related to events, no to internal schedulling.
Problems easier to track down

Events faster than threads on single CPU
No locking overheads
No context switching
Events more portable than threads
Threads provide true concurrency
Can have long-running stateful handlers without freezes
Scalable performance on multiple CPUS



Platform|Asynchronous Event-driven
------------ | -------------
Lock application / request with listener-workers threads | only one thread, which repeatedly fetches an event
Using incoming-request model| Using queue and then processes it
multithreaded server might block the request which might involve multiple events| manually saves state and then goes on to process the next event
Using context switching|no contention and no context switches
Using multithreading environments where listener and workers threads are used frequently to take an incoming-request lock|Using asynchronous I/O facilities (callbacks, not poll/select or O_NONBLOCK) environments

## Why Thread Are A Bad Idea
(for high-concurrency servers)

Performance : Many attempts to use threads for high concurrency have not performed well.
Control Flow: Threads have restrictive control flow

Synchronization: Thread synchronization mechanisms are too heavyweight

State Management: Threads stacks are an ineffective way to manage live state

Scheduling: The virtual processor model provided by threads forces the runtime system to be too generic and prevents it from making optimal schedulling decisions 


## Performance and Utilization

The http object encapsulates the HTTP protocol and its http.createServer method creates a whole web server, listening on the port specified in the .listen method. Every request (whether a GET or PUT on any URL) on that web server calls the provided function. It is very simple lightweight. In this case, regardless of the URL, it returns a simple text/plain “Hello World” response. 

Because of its minimal nature, this simple application should demonstrate the maximum request throughput of Node. Indeed many have published benchmark studies starting from this simplest of HTTP servers. 

## System Requirements

Node runs best on the POSIX-like operating systems. These are the various UNIX derivatives (Solaris, and so on) or workalikes (Linux, Mac OS X, and so on).

While Windows is not POSIX compatible, Node can be built on it either using POSIX compatibility environments (in Node 0.4x and earlier). 


## Node Js VS Apache

1. It's fast
1. It can handle tons of concurrent requests
1. It's written in JavaScript (which means you can use the same code server side and client side)

Platform|Number of request per second
------------ | -------------
PHP ( via Apache) | 3187,27
Static ( via Apache ) | 2966,51
Node.js |  5569,30


 
Lock application / request with listener-workers threads |  only one thread, which repeatedly fetches an event
Using incoming-request model  |  Using queue and then processes it
multithreaded server might block the request which might involve multiple events|manually saves state and then goes on to process the next event
Using context switching|no contention and no context switches
Using multithreading environments where listener and workers threads are used frequently to take an incoming-request lock|Using asynchronous I/O facilities (callbacks, not poll/select or O_NONBLOCK) environments


#### Node.js is a great tool for creating and running application logic that produces the core, variable content for your web page. But it’s not so great for serving static content – images and JavaScript files, for example – or load balancing across multiple servers.

##### To get the most out of Node.js, you need to cache static content, to proxy and load balance among multiple application servers, and to manage port contention between clients, Node.js, and helpers, such as servers running Socket.IO. NGINX can be used for all of these purposes, making it a great tool for Node.js performance tuning.


1. Implement a reverse proxy server

![GitHub Logo](1.png)
 

1. Cache static files
1. Load balance traffic across multiple servers
1. Proxy WebSocket connections

![GitHub Logo](4.png)
 

1. Implement SSL/TLS and HTTP/2

![GitHub Logo](5.png)
 


 

