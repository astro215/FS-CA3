---

## Handling APIs in React with Express and FastAPI

### Introduction

Welcome to our session on handling APIs in React. Today, we will learn about integrating React with Express and FastAPI to create dynamic web applications.

### Table of Contents

1. [What are APIs?](#what-are-apis)
2. [Why Use APIs?](#why-use-apis)
3. [Setting Up the Backend](#setting-up-the-backend)
   - [Express Setup](#express-setup)
   - [FastAPI Setup](#fastapi-setup)
4. [Creating the React Frontend](#creating-the-react-frontend)
   - [React Features for API Handling](#react-features-for-api-handling)
5. [Best Practices for API Interaction](#best-practices-for-api-interaction)
6. [Demo and Testing](#demo-and-testing)
7. [Conclusion](#conclusion)

---

### What are APIs?

API stands for Application Programming Interface. It is a set of rules that allows different software entities to communicate with each other. APIs enable an application to interact with external software components, operating systems, or microservices. They allow your application to access a feature or data from another service, application, or platform without requiring a complete understanding of their implementation.

---

### Why Use APIs?

- **Integration and Extension**: APIs are critical in connecting and extending functionalities of different software systems.
- **Automation**: They allow for the automation of tasks, enabling systems to communicate and operate with each other without human intervention.
- **Efficiency**: Using APIs, developers can leverage existing platform functionalities rather than build from scratch, significantly speeding up the development process.
- **Flexibility**: APIs provide the flexibility to build, innovate, and adapt features that can evolve with changing tech landscapes.

---

### Setting Up the Backend

#### Express Setup

1. **Installation**
   ```bash
   npm init -y
   npm install express cors
   ```

2. **Create a Simple Server with CORS**
   ```javascript
   const express = require('express');
   const cors = require('cors');
   const app = express();

   app.use(cors());

   app.get('/api/data', (req, res) => {
       res.json({ message: 'Hello from Express!' });
   });

   const PORT = process.env.PORT || 3000;
   app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
   ```

#### FastAPI Setup

1. **Installation**
   ```bash
   pip install fastapi uvicorn[standard] python-multipart
   ```

2. **Create API Endpoints with CORS**
   ```python
   from fastapi import FastAPI
   from fastapi.middleware.cors import CORSMiddleware

   app = FastAPI()

   app.add_middleware(
       CORSMiddleware,
       allow_origins=["*"],
       allow_credentials=True,
       allow_methods=["*"],
       allow_headers=["*"],
   )

   @app.get("/api/data")
   async def get_data():
       return {"message": "Hello from FastAPI!"}
   ```

3. **Running FastAPI Server**
   ```bash
   uvicorn main:app --reload
   ```

---

### Creating the React Frontend

#### App.js Implementation

```javascript
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function App() {
    const [dataFromExpress, setDataFromExpress] = useState('Loading...');
    const [dataFromFastAPI, setDataFromFastAPI] = useState('Loading...');

    useEffect(() => {
        // Fetching data using fetch from Express
        fetch('http://localhost:3000/api/data')
            .then(response => response.json())
            .then(data => setDataFromExpress(data.message))
            .catch(error => {
                console.error('Error fetching data from Express:', error);
                setDataFromExpress('Failed to load data');
            });

        // Fetching data using axios from FastAPI
        axios.get('http://localhost:8000/api/data')
            .then(response => {
                setDataFromFastAPI(response.data.message);
            })
            .catch(error => {
                console.error('Error fetching data from FastAPI:', error);
                setDataFromFastAPI('Failed to load data');
            });
    }, []);

    return (
        <div>
            <h1>React and API Integration Example</h1>
            <h2>Data from Express:</h2>
            <p>{dataFromExpress}</p>
            <h2>Data from FastAPI:</h2>
            <p>{dataFromFastAPI}</p>
        </div>
    );
}

export default App;
```

#### React Features for API Handling

- **useState**: Manages state in functional components.
- **useEffect**: Handles side-effects in functional components such as data fetching, subscriptions, or manually changing the DOM.
- **useContext**: Provides a way to pass data through the component tree without having to pass props down manually at every level.
---
#### Why Axios?

Axios is a promise-based HTTP client for the browser and Node.js that provides many features out-of-the-box, making it a powerful tool for API calls:

---
-   **Interceptors**: Allows you to alter the request or response entirely before they are handled by `.then` or `.catch`. This is particularly useful for authentication, logging, or adding custom headers.
-   **Automatic JSON transformation**: Automatically transforms JSON data into JavaScript objects and vice versa, simplifying the handling of JSON data.
-   **Cancellation**: Offers API cancellations through cancel tokens, which can be useful in complex UIs where multiple requests may need to be canceled to prevent unnecessary processing.
-   **Better error handling**: Provides rich error information including response code, headers, and more, which can be extremely useful for debugging and user feedback.
-   **Timeouts**: Easily configure how long Axios should wait for a response before aborting the request, preventing user interfaces from being stuck in an indefinite wait state.

---

### Why Use `useEffect` for API Calls?

Using `useEffect` for API calls instead of doing it directly in the component body or other lifecycle methods has several advantages:

-   **Separation of Concerns**: It keeps the component logic clean and focused on UI rendering and event handling, while side effects are managed separately.
-   **Handling Asynchronous Operations**: `useEffect` handles async operations gracefully and ensures that the component updates correctly after data is fetched.
-   **Avoiding Memory Leaks**: By using cleanup functions and correctly specifying dependencies, `useEffect` can help avoid memory leaks when the component unmounts or when subsequent effects are run.

Overall, `useEffect` provides a declarative approach to managing side effects in functional components, encapsulating behaviors that need to happen at specific times during a component’s lifecycle, such as after it first renders or after it updates.

### Best Practices for API Interaction

- **Error Handling**: Implement error handling to manage unexpected failures during API calls.
- **Loading States**: Maintain UI states for loading data to improve user experience.
- **Use Environment Variables**: Store API URLs and other sensitive details in environment variables.

---

### Demo and Testing

Live demo of React app fetching data from both Express and FastAPI. Ensure both servers are up and responding to API requests.

---

### Conclusion

Today we covered how to set up Express and FastAPI backends with CORS enabled and how to connect them with a React frontend using both Fetch and Axios. We also discussed best practices for API interaction and the advantages of using Axios for API calls.

Explore the code further on your own!

---

## Author

- Name - Jainil Patel
- PRN - 21070126039
- Batch - AIML A2
---

## References

- https://medium.com/womenintechnology/what-are-the-different-types-of-hooks-in-react-470fdeb86b9
- https://blog.logrocket.com/axios-vs-fetch-best-http-requests/
