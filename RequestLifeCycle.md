the largest waste with current programming technologies comes from waiting for I/O to complete. 
synchronous: you handle one request at a time, each in turn. pros: simple cons: any one request can hold up all the other requests
fork a new process: you start a new process to handle each request. pros: easy cons: does not scale well, hundreds of connections means hundreds of processes. fork() is the Unix programmer's hammer. Because it's available, every problem looks like a nail. It's usually overkill
threads: start a new thread to handle each request. pros: easy, and kinder to the kernel than using fork, since threads usually have much less overhead cons: your machine may not have threads, and threaded programming can get very complicated very fast, with worries about controlling access to shared resources.
https://www.npmjs.com/package/lifecycle-node
When Node receives an HTTP request, it creates the req and res objects (which begin their life as instances of http.IncomingMessage and http.ServerResponse respectively). The intended purpose of those objects is that they live as long as the HTTP request does. That is, the client makes an HTTP request, the req and res objects are created, a bunch of stuff happens, and finally a method on res is invoked that sends an HTTP response back to the client, and at that point the objects are no longer needed.

Because of Node's asynchronous nature, there could be multiple req and res objects at any given time, distinguished only by the scope in which they live. This may sound confusing, but in practice, you never have to worry about that: when you write your code, you write it as if you were always ever dealing with one HTTP request, and your framework (Express, for example), manages multiple requests.

JavaScript does indeed have a garbage collector, which eventually deallocates objects after their reference count drops to zero. So for any given request, as long as there's a reference to the req object (for example), that object will not be deallocated. Here's a simple example of an Express program that always saves every request (this is a terrible idea, by the way):

var allRequests = [];
app.use(function(req, res, next) {
    allRequests.push(req);
    next();
});
The reason this is a terrible idea is that if you never remove objects from allRequests, your server will eventually run out of memory as it processes traffic.

Typically, with Express, you'll rely on asynchronous functions that invoke a callback once they've done their work. If the callback function has a reference to the req or res objects, they will not be deallocated until the asynchronous function completes and the callback executes (and all other references are out of scope, naturally). Here's a simple example that just generates an artificial delay:

app.get('/fast', function(req, res) {
    res.send('fast!');
});

app.get('/slow', function(req, res) {
    setTimeout(function() {
        res.send('sloooooow');
    }, 3000);
});
If you navigate to /slow, your browser will spin for 3 seconds. In another browser, if you access /fast a bunch of times, you'll find that it still works. That's because Express is creating a req and  res object for each request, none of which interfere with each other. But the res object associated with the /slow request is not deallocated because the callback (which is holding a reference to that instance) hasn't executed.

At the end of the day, I feel like you're overthinking things. It's good to understand the fundamentals, certainly, but for the most part, reference counting and garbage collection in JavaScript is not something you have to think about or manage.
