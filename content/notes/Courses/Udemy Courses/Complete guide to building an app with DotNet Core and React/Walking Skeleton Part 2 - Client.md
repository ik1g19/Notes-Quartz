# Concepts

#react #udemy-course
# Creating the React Project

Rather than using HTML or CSS to build our web pages, we will build them using React components

We will be using `Vite` as opposed to `NextJS` etc... as the framework to create the React project

Using `npm` you can create a Vite project using

```
npm create vite@latest
```

First you will be prompted to enter a Vite project name

Then you will be prompted to select a framework for this project, which in this case will be React

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20240421234846.png|400]]

You will then be prompted to choose a variant, which in this case will be using TypeScript and **S**peedy **W**eb **C**ompiler

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20240421234944.png|400]]

Then `cd ./client-app` and run `npm install` to install all the dependencies needed

Start the Vite-React application using:

```
npm run dev
```

It will start on localhost:5173 by default

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20240421235132.png]]

# Reviewing the React Project Files

![[Images/Pasted image 20241103200114.png|150]]

- `node_modules` contains all of the dependencies the project is using
	- It gets the dependencies from `package.json`
- `index.html` is the boilerplate HTML
	- Default React scripts are loaded through`<script type="module" src="/src/main.tsx"></script>`
- `vite.config.ts` is the Vite configuration file
- `tsconfig.json` is for typescript configuration
- We use `public` for images etc.

You can add a script to `client-app\package.json` and then trigger it with `npm [name]`

📁`client-app\package.json`
```json
"scripts": {
    "start": "vite",
    "dev": "vite",
    "build": "tsc && vite build",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
```

We replace the default React page with this

📁`client-app\src\App.tsx`
```tsx
import './App.css'

function App() {

  return (
    <h1>Reactivies</h1>
  )
}

export default App
```

We can remove all the default styling as well by deleting everything inside `client-app\src\App.css` and `client-app\src\index.css`

We can change the server port with

📁`client-app\vite.config.ts`
```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react-swc'

// https://vitejs.dev/config/
export default defineConfig({
  server: {
    port: 3000
  },
  plugins: [react()],
})
```

# React Components

How React components work

![[Images/20241104_220006.jpg]]
## Virtual DOM

Virtual Domain Object Model

Kept in memory and synced with the real DOM via React

![[Images/camera_capture.jpg]]

Data cannot flow backwards from DOM to VDOM in React

## JSX

Sugar coating over JavaScript, that makes it look like html

## React Hooks

Hooks are functions that let us hook into Reacts state and lifecycle features

Common hooks
- `useState()` this will track state inside the component
	- A function component is a function that returns JSX
- `useEffect()` adds a side effect to our function so that something happens when our component mounts

# Typescript Components

## Typescript Features

| Pros                                 | Cons              |
| ------------------------------------ | ----------------- |
| Strong Typing                        | More Upfront Code |
| Object Oriented                      |                   |
| Access Modifiers                     |                   |
| Catches Mistakes Weak Typing Doesn't |                   |
# TypeScript Demo & Basics

[[notes/Uni Content/Advanced Programming Language Concepts/Week 3/Gradual Typing#Union Type|Union Typing]] allows multiple possible types

```ts
let data: number | string = 42

data = '42'
```

# Using TypeScript with React

Only one thing can be returned at a time in JSX

```tsx
import './App.css'

function App() {

  return (
    <h1>Reactivies</h1>
  )
}

export default App
```

When we want to use Java or TypeScript in a JSX element we use `{}`

The following example code demonstrates how TypeScript components can be used in React

`() => duck.makeSound` is wrapped in a callback method so that execution is deferred until the button is actually clicked, otherwise it would be executed as soon as the page is loaded

When iterating through elements e.g. using `map`, a unique key needs to be provided, as seen in `<div key={duck.name}>`

📁`demo.ts`
```ts
interface Duck {
  name: string;
  numLegs: number;
  makeSound: (sound: string) => void;
}

const duck1: Duck = {
  name: 'huey',
  numLegs: 2,
  makeSound: (sound: string) => console.log(sound)
}

const duck2: Duck = {
  name: 'duey',
  numLegs: 2,
  makeSound: (sound: string) => console.log(sound)
}

duck1.makeSound('quack');
duck2.makeSound('sound');
```

📁`App.tsx`
```tsx
import './App.css'
import { ducks } from './demo'

function App() {
  return (
    <div>
      <h1>Reactivities</h1>
      {ducks.map(duck => (
        <div key={duck.name}>
          <span>{duck.name}</span>
          <button onClick={() => duck.makeSound(duck.name + ' quack')}>Make sound</button>
        </div>
      ))}
    </div>
  )
}

export default App
```

This next example shows how to use a React component

The component accepts a Prop as a parameter

📁`App.tsx`
```tsx
import './App.css'
import { ducks } from './demo'

function App() {
  return (
    <div>
      <h1>Reactivities</h1>
      {ducks.map(duck => (
        <div key={duck.name}>
          <DuckItem key={duck.name} duck={duck} />
        </div>
      ))}
    </div>
  )
}

export default App
```

📁`DuckItem.tsx`
```tsx
import { Duck } from './demo'

interface Props {
  duck: Duck
}

export default function DuckItem({ duck }: Props) {
  return (
    <div key={duck.name}>
      <span>{duck.name}</span>
      <button onClick={() => duck.makeSound(duck.name + ' quack')}>Make sound</button>
    </div>
  )
}
```

# Web Extensions for Debugging

[React DevTools](https://addons.mozilla.org/en-GB/firefox/addon/react-devtools/)

# Fetching Data from the API

We will use Axios

>[!INFO]
>Axios is a _[promise-based](https://javascript.info/promise-basics)_ HTTP Client for `node.js` and the browser

To install run, and make sure to cd into the client app first

```
cd client-app
npm install axios
```

When the App component is rendered, we want the request to go to the API and fetch the data, and also for the component to store the data inside its own state

We will use the `useState` React hook to hold this information
- `const [activities, setActivities] = useState([]);`
- We provide a state that is going to be the value, `activities`, and a function to change the state `setActivities`
- The initial state is an empty array

When the component loads we want there to be a side effect, which is the request goes to the API to get the data to be stored in the state

We use `useEffect` to create a side effect (See )
- We provide it a callback function, which is the side effect code

We then loop over the retrieved activities

📁`client-app\src\App.tsx`
```tsx
import { useEffect, useState } from 'react'
import './App.css'
import axios from 'axios';

function App() {
  const [activities, setActivities] = useState([]);

  useEffect(() => {
    axios.get('http://localhost:5000/api/activities')
      .then(response => {
        setActivities(response.data)
      })
  }, [])

  return (
    <div>
      <h1>Reactivies</h1>
      <ul>
        {activities.map((activity: any) => (
          <li key={activity.id}>
            {activity.title}
          </li>
        ))}
      </ul>
    </div>
  )
}

export default App
```

Currently this will not work as it needs a CORS header

# CORS Policy

We go to our API and add a CORS policy

First we add the service

📁`API\Program.cs`
```cs
...
// Add services to the container.

builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
builder.Services.AddDbContext<DataContext>(opt => {
    opt.UseSqlite(builder.Configuration.GetConnectionString("DefaultConnection"));
});
//CORS Policy
builder.Services.AddCors(opt => {
    opt.AddPolicy("CorsPolicy", policy => {
        policy.AllowAnyHeader().AllowAnyMethod().WithOrigins("http://localhost:3000");
    });
});

var app = builder.Build();
...
```

Then we add the middleware
- The name has to match the service

📁`API\Program.cs`
```cs
...
// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseCors("CorsPolicy");

app.UseAuthorization();
...
```

# Semantic UI React

[Semantic UI](https://semantic-ui.com/) is a styling framework

Install and import

```
npm install semantic-ui-react semantic-ui-css
```

📁`client-app\src\main.tsx`
```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'
import 'semantic-ui-css/semantic.min.css'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

We can then use Semantic components in our app

📁`client-app\src\App.tsx`
```tsx
import { useEffect, useState } from 'react'
import './App.css'
import axios from 'axios';
import { Header, List } from 'semantic-ui-react';

function App() {
  const [activities, setActivities] = useState([]);

  useEffect(() => {
    axios.get('http://localhost:5000/api/activities')
      .then(response => {
        setActivities(response.data)
      })
  }, [])

  return (
    <div>
      <Header as='h2' icon='users' content='Reactivities'/>
      <List>
        {activities.map((activity: any) => (
          <List.Item key={activity.id}>
            {activity.title}
          </List.Item>
        ))}
      </List>
    </div>
  )
}

export default App
```