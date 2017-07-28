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









