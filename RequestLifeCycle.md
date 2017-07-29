 #  ![Node](https://heroku-elements.s3.amazonaws.com/buttons/uploaded_logos/000/002/550/icon/nodejs.png?1476395955) Request Life Cycle

**Request–response, or request–reply** is one of the basic methods computers use to communicate with each other, in which the first computer sends a request for some data and the second computer responds to the request.

The largest waste with current programming technologies comes from waiting for I/O to complete. 

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



