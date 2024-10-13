#node-js #udemy-course #javascript 

# NodeJS

## Creating a Server

Create a server with `createServer`

```Node
const http = require('http');

const server = http.createServer((req, res) => {
	console.log(req);
});

server.listen(3000)
```

`createServer` accepts a function with two parameters, request and response
- This is the request and how the server should respond

Then calling `listen` will start the event loop on the specified port

## Understanding Requests

Headers in a http request contain metadata about the request

```Node
req.url
```

## Sending Responses

```Node
const server = http.createServer((req,res) => {
	console.log(req.url, req.method, req.headers);

	res.setHeader('Content-Type', 'text/html');
	res.write('<html>');
	res.write('<head><title>My First Page</title></head>');
	res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
	res.write('</html>');
	res.end();
});

server.listen(3000);
```

## Routing Requests

```Node
const server = http.createServer((req, res) => {
  const url = req.url;
  const method = req.method;
  if (url === '/') {
    res.write('<html>');
    res.write('<head><title>Enter Message</title><head>');
    res.write('<body><form action="/message" method="POST"><input type="text" name="message"><button type="submit">Send</button></form></body>');
    res.write('</html>');
    return res.end();
  }
  if (url === '/message' && method === 'POST') {
    fs.writeFileSync('message.txt', 'DUMMY');
    res.statusCode = 302;
    res.setHeader('Location', '/');
    return res.end();
  }
  res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
});

server.listen(3000);
```

`302` is a redirect status code

## Parsing Request Bodies

![](notes/Courses/Udemy%20Courses/NodeJS%20-%20The%20Complete%20Guide/Images/Pasted%20image%2020230920144619.png)

`on()` allows us to listen for certain events

```Node
...
if (url === '/message' && method === 'POST') {
    const body = [];
    req.on('data', (chunk) => {
      console.log(chunk);
      body.push(chunk);
    });
    req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFileSync('message.txt', message);
    });
    res.statusCode = 302;
    res.setHeader('Location', '/');
    return res.end();
  }
...
```

The request body is read in chunks

On finishing reading the last chunk `end` is executed

The parsed body is then concatenated together

## Understanding Event Driven Code Execution

Sometimes functions passed as parameters will be executed asynchronously (later)

## Single Thread, Event Loop and Blocking Code

![](notes/Courses/Udemy%20Courses/NodeJS%20-%20The%20Complete%20Guide/Images/Pasted%20image%2020230920150931.png)

![](notes/Courses/Udemy%20Courses/NodeJS%20-%20The%20Complete%20Guide/Images/Pasted%20image%2020230920151347.png)

`refs` increments by 1 for every new callback that is registered, and reduces it by 1 for every event listener it doesn't need anymore

## Using Node Modules

`app.js`

```Node
const http = require('http');

const routes = require('./routes');

console.log(routes.someText);

const server = http.createServer(routes.handler);

server.listen(3000);
```

`routes.js`

```Node
const fs = require('fs');

const requestHandler = (req, res) => {
  const url = req.url;
  const method = req.method;
  if (url === '/') {
    res.write('<html>');
    res.write('<head><title>Enter Message</title></head>');
    res.write(
      '<body><form action="/message" method="POST"><input type="text" name="message"><button type="submit">Send</button></form></body>'
    );
    res.write('</html>');
    return res.end();
  }
  
  if (url === '/message' && method === 'POST') {
    const body = [];
    req.on('data', chunk => {
      console.log(chunk);
      body.push(chunk);
    });
    return req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFile('message.txt', message, err => {
        res.statusCode = 302;
        res.setHeader('Location', '/');
        return res.end();
      });
    });
  }
  res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
};

// module.exports = requestHandler;

// module.exports = {
//     handler: requestHandler,
//     someText: 'Some hard coded text'
// };

// module.exports.handler = requestHandler;
// module.exports.someText = 'Some text';

exports.handler = requestHandler;
exports.someText = 'Some hard coded text';
```

## Summary

![](notes/Courses/Udemy%20Courses/NodeJS%20-%20The%20Complete%20Guide/Images/Pasted%20image%2020230920152401.png)
