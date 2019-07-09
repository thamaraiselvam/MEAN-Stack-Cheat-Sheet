# MEAN Stack Cheat-Sheet

Those who want to become a *Full Stack Developer* their first choice is **MEAN Stack** because it has a lot of scopes and easy to learn as well but preparing is hard so Here's a Cheat Sheet - Inspired by [The Technical Interview Cheat Sheet.md](https://gist.github.com/TSiege/cbb0507082bb18ff7e4b)

<p align="center">
  <img src="https://media.giphy.com/media/uGjzzKY4BhtKw/giphy.gif">
</p>

>
This list is meant to be both a quick guide and reference for further research into these topics. It's basically a summary of important topics, there's no way it can cover everything in depth.  It also will be available as a gist on Github for everyone to edit and add to.

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
