
# Building Your First Web App with Express.js - A Complete Guide

## Table of Contents
1. [Introduction](#introduction)
2. [What is Express.js?](#what-is-expressjs)
3. [Why Use Express.js?](#why-use-expressjs)
4. [Setting Up Your Environment](#setting-up-your-environment)
5. [Demo Project: Hello World App](#demo-project-hello-world-app)
6. [Expanding the Application](#expanding-the-application)
7. [Handling POST Requests](#handling-post-requests)
8. [Conclusion](#conclusion)

---

## Introduction
Welcome to this Express.js tutorial where we will build a simple web application from scratch. This guide is perfect for those new to Express or looking to solidify their understanding by building a real-world project.

## What is Express.js?
Express.js is a minimal and flexible Node.js web application framework that provides a robust set of features to develop web and mobile applications efficiently.

## Why Use Express.js?
- Simplifies server creation
- Fast and efficient
- Ideal for building APIs
- Supports a variety of middleware

## Setting Up Your Environment
Before we start coding, ensure you have the following installed:
- Node.js
- A text editor like VS Code
- Terminal access

### Initialize Node.js Project
First, create a new directory for your project and initialize it with npm:
```bash
mkdir myexpressapp
cd myexpressapp
npm init -y
```
This command creates a `package.json` file which will manage all dependencies.

### Install Express and Nodemon
To install Express, run:
```bash
npm install express
```
For development convenience, install `nodemon`:
```bash
npm install --save-dev nodemon
```
Edit `package.json` to add a start script:
```json
"scripts": {
  "start": "nodemon app.js"
}
```

## Demo Project: Hello World App
### Initial Setup
Create a new file named `app.js`:
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello World!');
});

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```
### Run the Server
To start the server using nodemon, run:
```bash
npm start
```
Visit `http://localhost:3000` in your browser to see the message.

## Expanding the Application
### Adding More Routes
Add a route for the About page:
```javascript
app.get('/about', (req, res) => {
  res.send('About Page');
});
```

### Using Middleware
Log every request to the console:
```javascript
app.use((req, res, next) => {
  console.log('Request URL:', req.originalUrl);
  console.log('Time:', Date.now());
  next();
});
```

## Handling POST Requests
### Handling Form Data
First, enable Express to handle URL-encoded data (form data):
```javascript
app.use(express.urlencoded({ extended: true }));
```

Create a form route and view:
```javascript
app.get('/form', (req, res) => {
  res.send('<form method="POST" action="/submit-form"><input type="text" name="username" /><button type="submit">Submit</button></form>');
});

app.post('/submit-form', (req, res) => {
  const username = req.body.username;
  res.send(`Received submission with username: ${username}`);
});
```

### Handling Multi-part Form Data
For handling file uploads, use the `multer` middleware:
```bash
npm install multer
```

Set up multer in your Express app:
```javascript
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });

app.post('/upload', upload.single('file'), (req, res) => {
  res.send('File uploaded successfully.');
});
```


## Conclusion
We've covered the basics of setting up an Express.js application, adding routes, handling different types of data, and working with files. Expand upon this foundation by integrating databases, adding authentication, and more.

## Author
- Name - Jainil Patel
- PRN - 21070126039
- Batch - AIML A2

