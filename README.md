# MEAN Stack Cheat-Sheet

Those who want to become a *Full Stack Developer* their first choice is **MEAN Stack** because it has a lot of scopes and easy to learn as well but preparing is hard so Here's a Cheat Sheet - Inspired by [The Technical Interview Cheat Sheet.md](https://gist.github.com/TSiege/cbb0507082bb18ff7e4b)

<p align="center">
  <img src="https://media.giphy.com/media/uGjzzKY4BhtKw/giphy.gif">
</p>

>
This list is meant to be both a quick guide and reference for further research into these topics. It's basically a summary of important topics, there's no way it can cover everything in depth.  It also will be available as on [Github](https://github.com/thamaraiselvam/MEAN-Stack-Cheat-Sheet) for everyone to edit and add to.

## What the heck is MEAN Stack

- MEAN is a user-friendly full-stack JavaScript framework ideal for building dynamic websites and applications.
- One of the main benefits of the MEAN stack is that a single language, JavaScript, runs on every level of the application, making it an efficient and modern approach to web development.
- MEAN is an acronym for **MongoDB**, **ExpressJS**, **AngularJS** and **Node.js**

## MongoDB

<p align="center">
  <img height="245" width="350" src="https://media.giphy.com/media/3otPoHMzdMgfZznjpe/giphy.gif">
</p>

### MongoDB Introduction

- #### *What is MongoDB and where to be used ?*

MongoDB is a type of NoSQL DB and used in the following applications such as unstable schema, need highly scalability and availability.  [Read More](https://www.mongodb.com/what-is-mongodb)

- #### *Difference between NoSQL and SQL ?*

| MySQL Terms           | MongoDB Terms|
| ----------------------|:-------------:|
| database              | database |
| table                 | collection |
| row                   | document or BSON document |
| column                | field |
| index                 | index |
| table joins           | embedded documents and linking |
| primary key Specify any unique column or column combination as the primary key.   | primary key In MongoDB, the primary key is automatically set to the _id field. |
| aggregation (e.g. group by)         | aggregation pipeline      |

 [Read more detailed comparison on MongoDB vs MySQL](https://www.mongodb.com/compare/mongodb-mysql)

### Install MongoDB

- #### *How to Install **MongoDB** and **Robo 3T**?*

[Install MongoDB]( https://docs.mongodb.com/manual/installation/) and  [Robo 3T](https://robomongo.org/download) (Robo 3T -formerly Robomongo is the free lightweight GUI for MongoDB enthusiasts)

- #### *How to Install the **mongoose** node module?*

[Mongoose](https://www.npmjs.com/package/mongoose) is MongoDB driver which connects MongoDB and Node.JS [Read Document](https://mongoosejs.com/docs/guide.html)

### Work with Mongoose

- #### *Start with Schema?*

Everything in Mongoose starts with a Schema. Each schema maps to a MongoDB collection and defines the shape of the documents within that collection.

```js
 var mongoose = require('mongoose');
  var Schema = mongoose.Schema;

  var blogSchema = new Schema({
    title:  String,
    author: String,
    body:   String,
    comments: [{ body: String, date: Date }],
    date: { type: Date, default: Date.now },
    hidden: Boolean,
    meta: {
      votes: Number,
      favs:  Number
    }
  });
  ```

- #### *Creating a Model?*

To use our schema definition, we need to convert our blogSchema into a Model we can work with. To do so, we pass it into mongoose.model(modelName, schema)

```js
var Blog = mongoose.model('Blog', blogSchema);
```

[Read More Mongoose guide](https://mongoosejs.com/docs/guide.html#definition)

### Basic CURD functions

> Mongoose models provide several static helper functions for CRUD operations.

- #### *[create()](https://mongoosejs.com/docs/api.html#model_Model.create)*

Save one or more Documents to the database

- #### *[insertMany()](https://mongoosejs.com/docs/api.html#model_Model.insertMany)*

Shortcut for validating an array of documents and inserting them into MongoDB if they're all valid. This function is faster than .create() because it only sends one operation to the server, rather than one for each document.

- #### *[findOne()](https://mongoosejs.com/docs/api.html#model_Model.findOne)*

Finds one document

- #### *[find()](https://mongoosejs.com/docs/api.html#model_Model.find)*

Finds documents

- #### *[updateOne()](https://mongoosejs.com/docs/api.html#model_Model.updateOne)*

Updates one document in the database without returning it.

- #### *[update()](https://mongoosejs.com/docs/api.html#model_Model.update)*

Same as update(), except it does not support the multi or overwrite options.

- #### *[updateMany()](https://mongoosejs.com/docs/api.html#model_Model.updateMany)*

Same as update(), except MongoDB will update all documents that match filter

- #### *[deleteOne()](https://mongoosejs.com/docs/api.html#model_Model.deleteOne)*

Deletes the first document that matches conditions from the collection.

- #### *[deleteMany()](https://mongoosejs.com/docs/api.html#model_Model.deleteMany)*

Deletes all of the documents that match conditions from the collection

Read more about  [Mongoose Queries](https://mongoosejs.com/docs/queries.html)

### Aggregation

> Aggregations are operations that process data records and return computed results

These are operations like sum, count, average, group etc where we need to generated grouped results out of collection.
MongoDB exposes a pipeline based framework for aggregations, which looks something like below and [Read more](https://mongoosejs.com/docs/api/aggregate.html#aggregate_Aggregate)

```js
Model.aggregrate([
   pipe1_operator : {...},
   pipe2_operator : {...},
   pipe3_operator : {...}
])
```

- #### *$group*

Count the number of Users Belonging To A Particular Region

- #### *$match*

$match acts as a where condition to filter out documents.

- #### *$project*

$project is used to add columns dynamically to the collection and use it for further aggregation.

- #### *count*

Count Number of User who belong to a certain region

- #### *distinct*

Find all distinct regions

There are many more pipeline operators than dicussed above, which can be seen [here](http://docs.mongodb.org/manual/reference/operator/aggregation/#aggregation-expression-operators)

## Node.JS

<p align="center">
  <img height="245" width="350" src="https://user-images.githubusercontent.com/6559664/60865631-0c56c600-a244-11e9-972e-c367bcff55f6.gif">
</p>

### What is Node.JS

- Node.js is a server-side platform (JavaScript runtime) built on [Chrome's V8 JavaScript engine](https://v8.dev/)
- It is an open source server environment and free
- It runs on various platforms (Windows, Linux, Unix, Mac OS X, etc.)

### Why Node.js

#### Asynchronous and Event Driven

All APIs of Node.js library are asynchronous, that is, non-blocking. It essentially means a Node.js based server never waits for an API to return data. The server moves to the next API after calling it and a notification mechanism of Events of Node.js helps the server to get a response from the previous API call.

#### Very Fast

Being built on Google Chrome's V8 JavaScript Engine, Node.js library is very fast in code execution.

#### Single Threaded but Highly Scalable

Node.js uses a single threaded model with event looping. Event mechanism helps the server to respond in a non-blocking way and makes the server highly scalable as opposed to traditional servers which create limited threads to handle requests. Node.js uses a single threaded program and the same program can provide service to a much larger number of requests than traditional servers like Apache HTTP Server

#### No Buffering

Node.js applications never buffer any data. These applications simply output the data in chunks.

### Where to use Node.js

Following are the areas where Node.js is proving itself as a perfect technology partner.

- I/O bound Applications
- Data Streaming Applications
- Data Intensive Real-time Applications (DIRT)
- JSON APIs based Applications
- Single Page Applications

*** It is not advisable to use Node.js for CPU intensive applications ***

### NPM

NPM is a package manager for the JavaScript programming language. It is the default package manager for Node.js and it is the world's largest Software Registry. It contains more than one million packages.

### Install Node.js and NPM

Simply download the [Installer](https://nodejs.org/en/#download) directly from the [nodejs.org](https://nodejs.org/en/) web site or follow the instructions for platform specific.

### Linux

#### Debian based distributions

Such as Debian, Ubuntu, Linux mint and Raspbian

```bash
sudo apt-get install nodejs npm
```

#### Arch Linux

```bash
pacman -S nodejs npm
```

#### MacOS

```bash
brew install node
```

#### Windows

Simply download the [Windows Installer](https://nodejs.org/en/#download) directly from the [nodejs.org](https://nodejs.org/en/) web site.

### Techical Depth

#### Single thread

Single threaded processes contain the execution of instructions in a single sequence. In other words, one command is processes at a time. [Read more about single thread vs multi thread](https://www.tutorialspoint.com/single-threaded-and-multi-threaded-processes)

#### Event Loop

The event loop is what allows Node.js to perform non-blocking I/O operations — despite the fact that JavaScript is single-threaded — by offloading operations to the system kernel whenever possible.

Since most modern kernels are multi-threaded, they can handle multiple operations executing in the background. When one of these operations completes, the kernel tells Node.js so that the appropriate callback may be added to the poll queue to eventually be executed

Read following links to learn more about Event Loop

[The Node.js Event Loop](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)

[What the heck is the event loop anyway? by Philip Roberts - JSConf EU](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

[Visualisation tool for event loop](http://latentflip.com/loupe/)

#### JavaScript Engine vs JavaScript Runtime

A **JavaScript engine** is a program or interpreter which reads our JavaScript code, produces machine code, and finally runs the machine code. It is landed in JavaScript runtimes like web browsers, Node.js, or even Java Runtime Environment (JRE). Like any other interpreters, its job is to read and execute code.

**JavaScript runtime** is another software. It uses JavaScript Engine and provides some additional functionalities as needed. The most common example of the runtime is the web browser. Probably the second most widely used runtime is Node.js.

[Read more here](https://medium.com/@misbahulalam/uncover-the-javascript-engine-vs-runtime-6556ef449634)

### ECMAScript

ECMAScript(ES) is a scripting-language **specification standard**ized by Ecma International. It was created to standardize JavaScript and new standards is released on every year.

[ES6 Features](http://es6-features.org/)
[ES7, ES8, ES9 Features](https://medium.com/@madasamy/javascript-brief-history-and-ecmascript-es6-es7-es8-features-673973394df4)

### Hello World in Node.js

Refer [express](#express) for hello world progam.

### Some Common NPM Packages

- [express](https://www.npmjs.com/package/express)
- [body-parser](https://www.npmjs.com/package/body-parser)
- [lodash](https://www.npmjs.com/package/lodash)
- [async](https://www.npmjs.com/package/async)
- [moment](https://www.npmjs.com/package/moment)
- [request](https://www.npmjs.com/package/request)

## REST API

<p align="center">
  <img height="245" width="350" src="https://media.giphy.com/media/e3NinswgSNdRu/giphy.gif">
</p>

### *What is REST API*

- A REST stands for Representational State Transfer is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data.

- REST is a style of software architecture. As described in a dissertation by Roy Fielding, REST is an "architectural style" that basically exploits the existing technology and protocols of the Web.

### *HTTP Methods*

RESTful APIs enable you to develop any kind of web application having all possible CRUD operations. REST guidelines suggest using a specific HTTP method on a specific type of call made to the server (though technically it is possible to violate this guideline, yet it is highly discouraged).

Use below-given information to find suitable HTTP method for the action performed by API.

- #### *HTTP GET*

Use GET requests to retrieve resource representation/information only – and not to modify it in any way

- #### *HTTP POST*

 POST methods are used to create a new resource into the collection of resources.

- #### *HTTP PUT*

Use PUT APIs primarily to update existing resource.

- #### *HTTP DELETE*

As the name applies, DELETE APIs are used to delete resources.

- #### *HTTP PATCH*

PATCH requests are to make partial update on a resource

Read more [HTTP Methods](https://restfulapi.net/http-methods/)

## Express

<p align="center">
  <img height="245" width="350" src="https://media.giphy.com/media/3oriNYQX2lC6dfW2Ji/giphy.gif">
</p>

- ### *What is Express*

Fast, unopinionated, minimalist web framework for node.

- ### *Installation*

[Follow this simple instructions by Express Community](http://expressjs.com/en/starter/installing.html)

- ### *Create Hello World REST API with Express*

```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

This app starts a server and listens on port 3000 for connections. The app responds with “Hello World!” for requests to the root URL (/) or route. Read [Express Guide](http://expressjs.com/en/guide/routing.html) to know more about Express Routing

## Angular

<p align="center">
  <img height="245" width="350" src="https://media.giphy.com/media/r7Y17m4862kdW/giphy.gif">
</p>

Note: Always Refer [Angular Docs](https://angular.io/docs)  for detailed explanation

### What is Angular

Angular is a TypeScript-based open-source web application framework for building mobile and desktop web applications

### Why Angular

- Angular was written in TypeScript, a superset of JavaScript that implements many new ES2016+ features.
- Awesome Command Line Interface (CLI)
- Develop across all platforms
- Speed, Performance and Scalability
- Incredible tooling
- Perfect for Single page Application

### Setup Angular

#### Step 1: Install Node.js

Angular requires Node.js version 10.9.0 or later. To install node.js, go to [Install Node](#where-to-use-nodejs)

#### Step 2: Install the Angular CLI

```bash
npm install -g @angular/cli
```

that's it you have installed Angular on your machine.

### Angular CLI

The Angular CLI is a command-line interface tool that you use to initialize, develop, scaffold, and maintain Angular applications. You can use the tool directly in a command shell.

Enter the following to list commands or options for a given command (such as generate) with a short description

```bash
ng help
ng generate --help
```

Know more about [Angular CLI](https://angular.io/cli)

### Create and Run an application

Now it is time create your first Angular application.

#### Create New Angular Application

Use `new` command to create a new application.

```bash
ng new my-first-project
```

and enter into created application `cd my-first-project`

Use `serve` to run application.

```bash
ng serve
```

In your browser, open [http://localhost:4200/](http://localhost:4200/) to see the new app run. When you use the ng serve command to build an app and serve it locally, the server automatically rebuilds the app and reloads the page when you change any of the source files.

### Fundamentals

#### Architecture

Angular is a platform and framework for building client applications in HTML and TypeScript. Angular is written in TypeScript. It implements core and optional functionality as a set of TypeScript libraries that you import into your apps.

#### Module

The basic building blocks of an Angular application are <strong>NgModules</strong>, which provide a compilation context for components. NgModules collect related code into functional sets; an Angular app is defined by a set of NgModules. An app always has at least a root module that enables bootstrapping, and typically has many more feature modules

Learn more about [Angular Modules](https://angular.io/guide/architecture-modules)

#### Component

Components define views, which are sets of screen elements that Angular can choose among and modify according to your program logic and data. Every component consist of selector, template and style. Template and style can be inline or separate files.

Learn more about [Angular components](https://angular.io/guide/architecture-components)

#### Services and DI

Components use services, which provide specific functionality not directly related to views. Service providers can be injected into components as dependencies, making your code modular, reusable, and efficient.

You can have sharable methods and data into services.

Learn more about [Angular Services](https://angular.io/guide/architecture-services)

#### Routing

Angular Routing helps to controll naviagation paths of application.
which helps to retain application state as well.

Learn more about [Angular Routings](https://angular.io/guide/router)

#### Lifecycle Hooks

- A component has a lifecycle managed by angular.

- Angular creates it, renders it, creates and renders its children, checks it when its data-bound properties change, and destroys it before removing it from the DOM.

- Angular offers lifecycle hooks that provide visibility into these key life moments and the ability to act when they occur.

#### Lifecycle sequence

After creating a component/directive by calling its constructor, Angular calls the lifecycle hook methods in the following sequence at specific moments:

- ngOnChanges()
- ngOnInit()
- ngDoCheck()
- ngAfterContentInit()
- ngAfterContentChecked()
- ngAfterViewInit()
- ngAfterViewChecked()
- ngOnDestroy()

Learn More about [Angular Lifecycle](https://angular.io/guide/lifecycle-hooks)

### File Structure

You can see that your angular application has dozens of files and folders. lets see what is purpose of them.

- e2e

e2e folder has all unit test files and you should write unit testing inside this dir only.

- src/app

This folder contains all our applcation codes such as components, services and so on.

- src/asset

This folder is for asset files such as images, fonts.

- src/environments

This is for environment configurations such as Devopment mode, Production mode.

- src/polyfills

All browser compatibility stuffs lies here.

- src/style.css

This style file is common for entire angular application. if you want to define a style for whole app, you can do here, such as theming styles.

- src/karma

Unit testing configuration file

- package.json

Package.json contains all npm and script related stuffs

- angular.json

This file contains meta related to angular application

- [tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)

Compiler Configuration for TypeScript

- [tslint.json](https://www.npmjs.com/package/tslint)

Linter Configurations

- [editorconfig](https://editorconfig.org/)

EditorConfig helps maintain consistent coding styles for multiple developers
