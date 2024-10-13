# Concepts

#react #html #css #javascript

---
# Describing the UI
## Components

React allows you to combine markup, CSS and JavaScript into components

```js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

The above shows a React component `Profile` inside another component `Gallery`

**All** React components have to begin with a **capital letter**

This is what the browser sees by the end:

```html
<section>
	<h1>Amazing scientists</h1>
	<img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
	<img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
	<img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
</section>
```

Components are regular javascript functions, so multiple functions can be kept in the same file
- You cannot nest React component definitions

## Import/Exports

You can import/export components in the following way

```js
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

export default function App() {
  return (
    <Profile />
  );
}
```

```js
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

Named imports are done using curly braces

## JSX

JSX is the name of the syntax that lets you write HTML-like markup inside a javascript file

Main rules of JSX:

- Only a single root element can be returned
	- So multiple elements must be wrapped in a div or empty tag
- All tags must be closed - no self-closing tags are allowed
- Many HTML and SVG attributes are written in camelCase due to reserved words
	- `class` = `className`
	- `stroke-width` = `strokeWidth`

You can reference javascript values using curly braces:

```js
export default function Avatar() {
  const avatar = 'https://i.imgur.com/7vQD0fPs.jpg';
  const description = 'Gregorio Y. Zara';
  return (
    <img
      className="avatar"
      src={avatar}
      alt={description}
    />
  );
}
```

You can pass javascript objects using double curly braces:

```js
export default function TodoList() {
  return (
    <ul style={{
      backgroundColor: 'black',
      color: 'pink'
    }}>
      <li>Improve the videophone</li>
      <li>Prepare aeronautics lectures</li>
      <li>Work on the alcohol-fuelled engine</li>
    </ul>
  );
}
```

## Props

React components use props to communicate with each other

They are parameters which can be any javascript value

You can pass props to a child component in the following way:

```js
import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <div>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi', 
          imageId: 'YfeOqp2'
        }}
      />
      <Avatar
        size={80}
        person={{
          name: 'Aklilu Lemma', 
          imageId: 'OKS67lh'
        }}
      />
    </div>
  );
}
```

```js
export function getImageUrl(person, size = 's') {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

React component functions can only accept a single argument - a props object

### Spread Syntax

If there are a lot of props to pass then you can pass all of the props of the parent class using the spread syntax

```js
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```

```js
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```

When you nest content inside a JSX tag, the parent component will receive that content in a prop called `children`

```js
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```

## Conditional Rendering

You can conditionally render elements using javascript flow control

```js
function Item({ name, isPacked }) {
  if (isPacked) {
    return <li className="item">{name} ✔</li>;
  }
  return <li className="item">{name}</li>;
}

export default function PackingList() {
  return (
    <section>
      <h1>Sally Ride's Packing List</h1>
      <ul>
        <Item 
          isPacked={true} 
          name="Space suit" 
        />
        <Item 
          isPacked={true} 
          name="Helmet with a golden leaf" 
        />
        <Item 
          isPacked={false} 
          name="Photo of Tam" 
        />
      </ul>
    </section>
  );
}
```

You can return null to render nothing:

```js
if (isPacked) {
  return null;
}
return <li className="item">{name}</li>;
```

You can use the conditional operator for rendering as well:

```js
return (
  <li className="item">
    {isPacked ? name + ' ✔' : name}
  </li>
);
```

### Logical And

Logical And `&&` can be used as a shortcut to conditionally render something

```js
return (
  <li className="item">
    {name} {isPacked && '✔'}
  </li>
);
```

A JavaScript `&&` expression returns the value of its right side (in our case, the checkmark) if the left side (our condition) is `true`. But if the condition is `false`, the whole expression becomes `false`. React considers `false` as a “hole” in the JSX tree, just like `null` or `undefined`, and doesn’t render anything in its place

