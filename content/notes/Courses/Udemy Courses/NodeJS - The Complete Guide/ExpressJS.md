
#udemy-course #express-js #javascript 

# Express.js

Simplifies server logic

Alternatives to Express:
- Adonis.js
- Koa
- Salis.js

import with `const express = require('express');`

Create the app with `express()`

The created app can be used as a request handler

```node
const app = express();
const server = http.createServer(app);
```

## Middleware

The function passed to `app.use((req, res, next) => {})` will be used to handle every request

`next` is a function that will be executed to allow the request to travel on to the next middleware

```node
app.use((req, res, next) => {
	console.log('In the middleware');
	next();
});

app.use((req, rest, next) => {
	console.log('Another middleware');
});
```

If `next` was not called then only the first middleware would be executed upon a request

`send()` is used to send responses (by default `text/html`)

```node
app.use((req, res, next) => {
	console.log('In the middleware');
	next();
});

app.use((req, rest, next) => {
	console.log('Another middleware');
	res.send('<h1>Test Header</h1>');
});
```

Instead of using:

```node
const server = http.createServer(app);
server.listen(3000);
```

We can use:

```node
app.listen(3000);
```

## Handling Different Routes

`app.use('/', (req, res, next) => {});` means that every routing starting with a `/` will be handled
- Not to be confused with exactly being the route `/`

So to handle a route whilst also handling the root path, you need to route the root path last

```node
app.use('/add-product', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>The "Add Product" Page</h1>');
});

app.use('/', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>Hello from Express!</h1>');
});
```

To have code that will execute every time:

```node
app.use('/', (req, res, next) => {
    console.log('This always runs!');
    next();
});

app.use('/add-product', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>The "Add Product" Page</h1>');
});

app.use('/', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>Hello from Express!</h1>');
});
```

## Parsing Incoming Requests

Package needed in order to parse requests:

```
npm install --save body-parser
```

And import with:

```node
const bodyParser = require('body-parser');
```

To then parse the request you pass it to the app handler:

```node
app.use(bodyParser.urlencoded({extended: false}));

app.use('/add-product', (req, res, next) => {
  res.send('<form action="/product" method="POST"><input type="text" name="title"><button type="submit">Add Product</button></form>');
});

app.post('/product', (req, res, next) => {
    console.log(req.body);
    res.redirect('/');
});

app.use('/', (req, res, next) => {
  res.send('<h1>Hello from Express!</h1>');
});
```

`app.use` would be used for every request, regardless of if it was GET or POST

So to filter requests we use `app.get` or `app.post`

## Using Express Router

Typically we want to split our routing code over multiple files

Routing related code typically goes under the `routes` folder

Add `admin.js` and `shop.js`
- These will control routing for normal and admin users

Create an express router with `const router = express.Router()`

Use this to handle the admin requests in `admin.js`:

```node
app.use('/add-product', (req, res, next) => {
  res.send('<form action="/product" method="POST"><input type="text" name="title"><button type="submit">Add Product</button></form>');
});

app.post('/product', (req, res, next) => {
    console.log(req.body);
    res.redirect('/');
});

app.use('/', (req, res, next) => {
  res.send('<h1>Hello from Express!</h1>');
});
```

And in `shop.js`:

```node
const express = require('express');

const router = express.Router();

router.get('/', (req, res, next) => {
  res.send('<h1>Hello from Express!</h1>');
});

module.exports = router;
```

We can then `require` the exported modules from the main app and `use` the routing:

```node
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

const adminRoutes = require('./routes/admin');
const shopRoutes = require('./routes/shop');

app.use(bodyParser.urlencoded({extended: false}));

app.use(adminRoutes);
app.use(shopRoutes);

app.listen(3000);
```

## Adding a 404 Page

We want to add a 'catch all' middleware at the bottom

```node
...
app.use(adminRoutes);
app.use(shopRoutes);

app.use((req, rest, next) => {
	res.status(404).send('<h1>Page not found</h1>');
})

app.listen(3000);
```

## Filtering Paths

You can filter by paths at the `use` level

```node
app.use('/admin', adminRoutes);
app.use(shopRoutes);
```

This means that any paths after this will be /admin/path

```node
router.get('/add-product', (req, res, next) => {
  res.send(
    '<form action="/admin/add-product" method="POST"><input type="text" name="title"><button type="submit">Add Product</button></form>'
  );
});

router.post('/add-product', (req, res, next) => {
  console.log(req.body);
  res.redirect('/');
});
```

It is not necessary to repeat /admin once it has been filtered

So the examples above are actually for /admin/add-product

## Creating and Serving HTML Pages

Create a folder called `views` to contain HTML files you want to serve

Example:

`add-product.html`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Add Product</title>
</head>

<body>
    <header>
        <nav>
            <ul>
                <li><a href="/">Shop</a></li>
                <li><a href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <form action="/add-product" method="POST">
            <input type="text" name="title">
            <button type="submit">Add Product</button>
        </form>
    </main>
</body>

</html>
```

`shop.html`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Add Product</title>
</head>

<body>
    <header>
        <nav>
            <ul>
                <li><a href="/">Shop</a></li>
                <li><a href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <h1>My Products</h1>
        <p>List of all the products...</p>
    </main>
</body>

</html>
```

We can now serve these HTML pages using `sendFile`

By default `/` references the root directory on the operating system, so `path` is used to reference the current working directory

`admin.js`

```node
const path = require('path');

const express = require('express');

const router = express.Router();

// /admin/add-product => GET
router.get('/add-product', (req, res, next) => {
  res.sendFile(path.join(__dirname, '../', 'views', 'add-product.html'));
});

// /admin/add-product => POST
router.post('/add-product', (req, res, next) => {
  console.log(req.body);
  res.redirect('/');
});

module.exports = router;
```

`shop.js`

```node
const path = require('path');

const express = require('express');

const router = express.Router();

router.get('/', (req, res, next) => {
  res.sendFile(path.join(__dirname, '../', 'views', 'shop.html'));
});

module.exports = router;
```

## Serving File Statically

Create a folder `public` to hold all the files accessible to the client

This folder will hold css content for pages

Serving files **statically** - Serving files not through the router, but directly from the file system

Use:

```node
app.use(express.static(path.join(__dirname, 'public')));
```

To grant 'read access' (serve statically) the public folder

When referencing the stylesheet, you do not need to include /public as node will already be working within this folder as the folder `public` is being served

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Add Product</title>
    <link rel="stylesheet" href="/css/main.css">
</head>

<body>
    <header class="main-header">
        <nav class="main-header__nav">
            <ul class="main-header__item-list">
                <li class="main-header__item"><a class="active" href="/">Shop</a></li>
                <li class="main-header__item"><a href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <h1>My Products</h1>
        <p>List of all the products...</p>
    </main>
</body>

</html>
```

## Summary

![](notes/Courses/Udemy%20Courses/NodeJS%20-%20The%20Complete%20Guide/Images/Pasted%20image%2020230925215649.png)
