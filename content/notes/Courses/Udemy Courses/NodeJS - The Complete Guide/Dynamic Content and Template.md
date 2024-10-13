#udemy-course #templating

---
# Dynamic Content and Templating

## Templating Engines

![](notes/Courses/Udemy%20Courses/NodeJS%20-%20The%20Complete%20Guide/Images/Pasted%20image%2020230925220915.png)

### Available Engines

![](notes/Courses/Udemy%20Courses/NodeJS%20-%20The%20Complete%20Guide/Images/Screenshot%20from%202023-09-25%2022-11-27.png)

## Installing and Implementing Pug

`npm install --save ejs pug express-handlebars`

`app.set` allows us to set a global configuration value

```node
app.set('view engine', 'pug');
```

The default locations for views is `/views/`

We can specify a custom location with:

```node
app.set('views', 'views');
```

Create `shop.pug` under `views/` - this will hold the template that pug will convert to HTML

`shop.pug`

```
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        meta(http-equiv="X-UA-Compatible", content="ie=edge")
        title My Shop
        link(rel="stylesheet", href="/css/main.css")
        link(rel="stylesheet", href="/css/product.css")
    body
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a.active(href="/") Shop
                    li.main-header__item
                        a(href="/admin/add-product") Add Product
```

Since this is now using a templating engine, we don't use `sendFile`

We now use `render` (in `shop.js`):

```node
router.get('/', (req, res, next) => {
  res.render('shop');
});
```

## Outputting Dynamic Content

We can share variables between requests by exporting them (`admin.js`):

```node
const path = require('path');

const express = require('express');

const rootDir = require('../util/path');

const router = express.Router();

const products = [];

// /admin/add-product => GET
router.get('/add-product', (req, res, next) => {
  res.sendFile(path.join(rootDir, 'views', 'add-product.html'));
});

// /admin/add-product => POST
router.post('/add-product', (req, res, next) => {
  products.push({ title: req.body.title });
  res.redirect('/');
});

exports.routes = router;
exports.products = products;
```

And then requiring them (`shop.js`):

```node
const path = require('path');

const express = require('express');

const rootDir = require('../util/path');
const adminData = require('./admin');

const router = express.Router();

router.get('/', (req, res, next) => {
  const products = adminData.products;
  res.render('shop', {prods: products, docTitle: 'Shop'});
});

module.exports = router;
```

We can pass dynamic content to the `render` function as a js object with key-value pairs

In this case we are passing a list of products, which hold a value `title`

We can then handle this content in `shop.pug`:

```
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        meta(http-equiv="X-UA-Compatible", content="ie=edge")
        title #{docTitle}
        link(rel="stylesheet", href="/css/main.css")
        link(rel="stylesheet", href="/css/product.css")
    body
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a.active(href="/") Shop
                    li.main-header__item
                        a(href="/admin/add-product") Add Product

        main
            if prods.length > 0
                .grid
                    each product in prods
                        article.card.product-item
                            header.card__header
                                h1.product__title #{product.title}
                            div.card__image
                                img(src="link_to_image", alt="A Book")
                            div.card__content
                                h2.product__price $19.99
                                p.product__description A very interesting book about so many even more interesting things!
                            .card__actions
                                button.btn Add to Cart
            else
                h1 No Products
```

We reference a variable in pug using `#{}` e.g. `#{docTitle}`

We then iterate through objects in pug with `each`

The `if` statement is used to catch the case where no objects have been added

## Using Pug Layouts

Create a `layouts` subfolder under `views`

This will contain the main layout of every page

`main-layout.pug`

```
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        meta(http-equiv="X-UA-Compatible", content="ie=edge")
        title #{pageTitle}
        link(rel="stylesheet", href="/css/main.css")
        block styles
    body   
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a(href="/", class=(path === '/' ? 'active' : '')) Shop
                    li.main-header__item
                        a(href="/admin/add-product", class=(path === '/admin/add-product' ? 'active' : '')) Add Product
        block content
```

`block` tags represent spaces where other pug files can extend the template and insert their own custom content

Inline ifs are used to add the `active` class if the path of the page matches parameter `path` that is passed to the render function e.g. in `shop.js`

```node
router.get('/', (req, res, next) => {
  const products = adminData.products;
  res.render('shop', {prods: products, pageTitle: 'Shop', path: '/'});
});
```

`add-product.pug`

```
extends layouts/main-layout.pug

block styles
    link(rel="stylesheet", href="/css/forms.css")
    link(rel="stylesheet", href="/css/product.css")

block content
    main
        form.product-form(action="/admin/add-product", method="POST")
            .form-control
                label(for="title") Title
                input(type="text", name="title")#title
            button.btn(type="submit") Add Product
```

`extends` is used to extend the pug template

Content is inserted into `block`s with the `block` tags

`404.pug`

```
extends layouts/main-layout.pug

block content
    h1 Page Not Found!
```

## Working with Handlebars

Uses normal HTML mixed with some templating logic

Importing:

```node
const expressHbs = require('express-handlebars');
```

Using:

```node
app.engine('hbs', expressHbs());
app.set('view engine', 'hbs');
```

Create a file with the extension of what you used in the above code, in this case `404.hbs`

Dynamic content is then passed through render as a key-value js object in the same way

Handlebar content is normal HTML code but dynamic content is represented with `{{}}`

```html
<title>{{ pageTitle }}</title>
```

Handlebars only supports True/False logic in its templating, so any calculations must be performed in js code and then passed to handlebar templating as a boolean

```node
res.render('shop', {prods: products, pageTitle: 'Shop', path: '/', hasProducts: products.length > 0})
```

```html
{{#if hasProducts}}
...
{{else}}
...
{{/if}}
```

You can iterate in handlebars with `each`

```html
{{#each prods}}
<h1 class="product_title">{{ this.title }}</h1>
{{/each}}
```

## Using Handlebar Layouts

`main-layout.hbs`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>{{ pageTitle }}</title>
    <link rel="stylesheet" href="/css/main.css">
    {{#if formsCSS}}
        <link rel="stylesheet" href="/css/forms.css">
    {{/if}}
    {{#if productCSS}}
        <link rel="stylesheet" href="/css/product.css">
    {{/if}}
</head>

<body>
    <header class="main-header">
        <nav class="main-header__nav">
            <ul class="main-header__item-list">
                <li class="main-header__item"><a class="{{#if activeShop }}active{{/if}}" href="/">Shop</a></li>
                <li class="main-header__item"><a class="{{#if activeAddProduct }}active{{/if}}" href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>
    {{{ body }}}
</body>

</html>
```

The only way to extend a layout is by inserting content into `{{{ body }}}`

So `if` statements have to be used to dynamically insert styles

e.g. `shop.js`:

```node
const path = require('path');

const express = require('express');

const rootDir = require('../util/path');
const adminData = require('./admin');

const router = express.Router();

router.get('/', (req, res, next) => {
  const products = adminData.products;
  res.render('shop', {
    prods: products,
    pageTitle: 'Shop',
    path: '/',
    hasProducts: products.length > 0,
    activeShop: true,
    productCSS: true
  });
});

module.exports = router;
```

Using handlebars in `app.js`:

```node
const path = require('path');

const express = require('express');
const bodyParser = require('body-parser');
const expressHbs = require('express-handlebars');

const app = express();

app.engine(
  'hbs',
  expressHbs({
    layoutsDir: 'views/layouts/',
    defaultLayout: 'main-layout',
    extname: 'hbs'
  })
);
app.set('view engine', 'hbs');
app.set('views', 'views');

const adminData = require('./routes/admin');
const shopRoutes = require('./routes/shop');

app.use(bodyParser.urlencoded({ extended: false }));
app.use(express.static(path.join(__dirname, 'public')));

app.use('/admin', adminData.routes);
app.use(shopRoutes);

app.use((req, res, next) => {
  res.status(404).render('404', { pageTitle: 'Page Not Found' });
});

app.listen(3000);
```

