# Schema and Schema-less Documents in MongoDB 

## Table of Contents
- [Introduction](#introduction)
- [What is MongoDB?](#what-is-mongodb)
- [Schema vs. Schema-less Design](#schema-vs-schema-less-design)
- [Demo Setup](#demo-setup)
- [Schema Model Coding Demo](#schema-model-coding-demo)
- [Schema-less Model Coding Demo](#schema-less-model-coding-demo)
- [Conclusion](#conclusion)


## Prerequisites 
- Node 
- JavaScript
- Mongo DB 

## Introduction
Welcome to our detailed exploration of MongoDB, focusing on the concepts of schema and schema-less data structures. This presentation will guide you through the basics of MongoDB, demonstrate the implementation of both data approaches, and discuss their advantages and disadvantages.

---

## What is MongoDB?
MongoDB is a document-oriented NoSQL database used for high volume data storage. Unlike relational databases that use tables and rows, MongoDB uses collections and documents.

### Key Features:
- **Document Oriented**: Stores data in JSON-like documents.
- **Schema-less Nature**: Offers flexibility to handle diverse and evolving data formats.
- **Scalability**: Designed to handle large data sets and heavy load.

---

## Schema vs. Schema-less Design

### What is a Schema?
In MongoDB, a schema represents the structure of data within documents of a collection. Although MongoDB is schema-less by nature, frameworks like Mongoose allow developers to impose a schema at the application level. This means defining what kind of data fields (and their types) documents can contain, along with validation rules and default values.

### Why Use a Schema?
- **Data Consistency**: Ensures all documents in a collection adhere to a predefined structure, making data easier to understand and manage.
- **Validation**: Enforces rules on the data being stored, which can prevent corrupt data or formatting errors from entering your database.
- **Ease of Maintenance**: With a clear structure, new developers or tools can quickly understand and interact with the data without needing to dig through individual records to determine what fields might exist.

### Schema Example:
In a blogging application, a post might always need a title, content, and author. Using a schema ensures that every post meets these requirements:

```javascript
const postSchema = new mongoose.Schema({
    title: { type: String, required: true },
    content: { type: String, required: true },
    author: { type: String, required: true },
    createdAt: { type: Date, default: Date.now }
});
```

### What is Schema-less?
Schema-less databases, like MongoDB, store documents in a collection without requiring a uniform structure. Each document can have different fields. The absence of a schema allows documents to be more flexible and dynamic.

### Why Use Schema-less?
- **Flexibility**: Easily adapt to changes in your application's data needs without needing to modify a centralized database schema.
- **Rapid Development**: Quicker iteration and deployment of new features since developers can store data without waiting for schema updates.
- **Heterogeneous Data**: Ideal for situations where data structure can vary widely or is unknown at the time of database design.

### Schema-less Example:
In the same blogging application, suppose you decide to allow users to add customized fields to their profiles, such as hobbies or skills:

```javascript
const userProfile = new mongoose.Schema({}, { strict: false });
const UserProfile = mongoose.model('UserProfile', userProfile);

const newUserProfile = new UserProfile({
    name: 'Alice',
    hobbies: ['Reading', 'Hiking'],
    skills: {
        writing: 'Advanced',
        coding: 'Beginner'
    }
});
```

This approach lets each user document hold different data according to the users' choices.

---

## When to Use Schema vs. Schema-less Design

Choosing between schema and schema-less should be guided by the specific requirements of your application and the nature of the data it handles.

### Consider Using a Schema When:
- You have well-defined data structures that are unlikely to change frequently.
- Data integrity and consistency are critical for the application’s functionality.
- You are dealing with a large scale application where the overhead of validating data structures in application code could be problematic.

### Consider Using Schema-less When:
- Your application needs to handle a variety of data types or the structure of data is dynamic.
- You are prototyping an application and are unsure of the final data structure.
- The application requires the flexibility to store data from different sources that might not follow the same structure.

## Demo Setup

First, let's set up a basic Node.js application to use MongoDB and Mongoose.

### Installation Commands:
```bash
mkdir mongodb-demo
cd mongodb-demo
npm init -y
npm install mongoose
```

### Connect to MongoDB:
Create a `connect.js` file to establish a MongoDB connection via Mongoose.

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase')
  .then(() => {
    console.log('connected to database')
    })
  .catch((err) => {
    console.log(err)
  }) 

```

---

## Schema Model Coding Demo

Let's define a schema model for a user collection using Mongoose.

### User Schema Definition:
```javascript
const userSchema = new mongoose.Schema({
    name: String,
    age: Number,
    email: { type: String, required: true }
});

const User = mongoose.model('User', userSchema);

const newUser = new User({
    name: 'John Doe',
    age: 30,
    email: 'johndoe@example.com'
});

newUser.save().then(doc  => {
	console.log('Document saved:', doc);
	}).catch(err  => {
	console.error('Error saving document:', err);
});
```

---

## Schema-less Model Coding Demo

Now, let's demonstrate inserting a document that does not strictly adhere to a predefined schema.

### Schema-less User Model:
```javascript
const userSchemaless = new mongoose.Schema({}, { strict: false });
const UserSchemaless = mongoose.model('UserSchemaless', userSchemaless);

const newUser = new UserSchemaless({
    name: 'John',
    hobby: 'Fishing' // Not defined in any schema
});
newUser.save().then(doc => {
    console.log('Document saved:', doc);
}).catch(err => {
    console.error('Error saving document:', err);
});
```

---

## Conclusion

Today, we explored MongoDB's flexible data handling through schema and schema-less designs. Each approach offers unique benefits and challenges, making MongoDB a versatile choice for developers dealing with diverse and evolving data sets.

---
## References
 - https://medium.com/@musasazib/mongoose-discusses-schema-and-model-work-81c5b4b73975
 - https://www.scaler.com/topics/mongoose-vs-mongodb/
 - https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/#std-label-install-mdb-community-windows
 - https://www.mongodb.com/docs/atlas/getting-started/#go-further-with-service
 - https://www.mongodb.com/docs/compass/current/query/queries/


## Author
- Name - Jainil Patel
- PRN - 21070126039
- Batch - AIML A2

