# Socket IO

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Real-Time Communication
- Socket IO

## Real-Time Communication

Real-time communication (RTC) is used to exchange information almost instantly with negligible latency, it allows data transmission in both directions simultaneously and an example of this would be voice calls, video calls, screen sharing, live chat, etc.

## What Is Socket IO

Socket IO is a library that is used for event-based real-time communications, it can be used to create applications that rely on bidirectional instant communication such applications that uses chat, instant notifications.

## Socket IO In The Backend

To use socket IO in the backend we need to install it with the following command `npm install socket.io`.

### Setting Up Connection

```js
const express = require("express");
const http = require("http");
const socket = require("socket.io");

const app = express();
const server = http.createServer(app);
const io = socket(server, { cors: { origin: "*" } });

const PORT = process.env.PORT || 5000;

server.listen(PORT, () => {
  console.log(`App listening at http://localhost:${PORT}`);
});

// setting up the connection
io.on("connection", (socket) => {
  // `socket.id` is the id assigned to the user that connected
  console.log(`${socket.id} is connected`);
});
```

### Receiving Events

```js
io.on("connection", (socket) => {
  // the first parameter is the event name, in this case the `message` event is a custom event
  // the second parameter is a callback function has access to the data sent to the server
  socket.on("message", (data) => {
    // well log the sent message
    console.log(data);
  });
});
```

### Emitting Events

```js
io.on("connection", (socket) => {
  // emits and event `connected` to everyone
  socket.emit("connected", `${socket.id} is connected`);

  socket.on("message", (data) => {
    // emits an event to all the connected clients with the value of the received message
    socket.broadcast.emit("message", data);
  });
});
```

## Socket IO In The Frontend

To use socket IO in the frontend we need to install it with the following command `npm install socket.io-client`.

### Connecting To The Server

- `.env` file in the frontend file

```env
# environment variable in react must start with the prefix REACT_APP
REACT_APP_SOCKET_URL=http://localhost:5000
```

```js
import React, { useState, useEffect } from "react";
// import io from socket.io-client"
import { io } from "socket.io-client";
// get the endpoint url from the .env file
const ENDPOINT = "REACT_APP_SOCKET_URL";

function App() {
  const [messages, setMessages] = useState([]);
  const [message, setMessage] = useState();
  // connect to the server, the connection can be made in a separate file (context, redux, exported) and used here
  const socket = io.connect(ENDPOINT);

  const sendMessage = () => {
    // emit a `message` event with the value of the message
    socket.emit("message", message);
  };

  useEffect(() => {
    // add a an event listener on message events
    socket.on("message", (data) => {
      setMessages((messages)=>[...messages, data])  
      });

    // remove all listeners on clean up
    return () => socket.removeAllListeners();
  }, []);

  return (
    <div>
      <input type="text" onChange={(e)=>{ setMessage(e.target.value)}}/>
      <button onClick={sendMessage}> Send </button>
      {messages.map((message, index) => {
            return <div key={index}> {message} </div>;
          })}
    </div>
  );
}

export default App;
```
