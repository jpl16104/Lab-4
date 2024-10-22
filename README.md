# CSE-2102 Lab 4: HTTP Calls, REST, and Token-Based Authentication

## Overview

This project illustrates how to construct a basic client-server system using HTTP requests, RESTful architecture, and token-based authentication with JWT (JSON Web Token). The system is composed of three main parts:

1. **Flask Server (`my-server.py`)**: A simple Flask server providing endpoints for login and echo functionalities.
2. **Client (`my-calls.py`)**: A client script that uses the `httpx` library to send HTTP GET and POST requests to the server.
3. **Token-Based Authentication**: Implements JWT for secure communication, ensuring that only authenticated users can access specific resources.

## Components

### 1. **Flask Server (`my-server.py`)**

The server is developed using Flask and offers two primary routes:
- **`/login`**: Processes login requests. When a valid user ID is received, the server creates a JWT token and sends it back to the client.
- **`/echo`**: Requires the client to include a valid JWT token in the `Authorization` header. The server verifies the token and, if it's valid, returns a message echoing the text sent by the client.

Key features:
- Generates tokens using JWT.
- Validates tokens to ensure they are valid and have not expired.

### 2. **Client (`my-calls.py`)**

The client utilizes the `httpx` library to interact with the server and performs the following tasks:
- **Login**: Sends a POST request to the `/login` endpoint to obtain a JWT token.
- **Echo**: Sends a POST request to the `/echo` endpoint, including the JWT token in the `Authorization` header. The server replies by echoing the text provided in the request.

Key features:
- Demonstrates how to make GET and POST requests.
- Manages JSON data transmission and handles token-based authentication.

### 3. **Token-Based Authentication**

JWT tokens are used for authorization. During the login process, a token is generated and then used to access protected routes like `/echo`. Tokens contain a user ID and an expiration time and are securely signed using a secret key on the server.

Key features:
- Provides secure communication through tokens.
- Checks tokens for validity and expiration with each protected request.

## System Diagram

Below is a simple diagram showing how the system works:


```
+---------------------+           +----------------------+
|      Client         |           |       Server          |
+---------------------+           +----------------------+
|                     |           |                      |
| 1. Login Request     +---------> | 2. Generate JWT      |
| (POST /login)        |           | and return token     |
|                     | <---------+                      |
| 3. Receive JWT       |           |                      |
|                     |           |                      |
| 4. Send Echo Request +---------> | 5. Verify Token      |
| (POST /echo)         |           | and return echo      |
| (with token)         | <---------+                      |
+---------------------+           +----------------------+
```

## How to Run the Project

1. **Start the Server**:
   ```bash
   python3 my-server.py
   ```
   
2. **Run the Client**:
   ```bash
   python3 my-calls.py
   ```

The client will:
1. Log in to receive a JWT token.
2. Use the token to make a request to the `/echo` endpoint.

## Conclusion

This project demonstrates the basics of building a RESTful service with token-based authentication using JWT. It can be expanded further with more complex authorization mechanisms and additional features such as token refresh, user roles, and more.
