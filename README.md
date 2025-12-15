# Realtime Chatting System (Basic Example)

This is a very basic example of a realtime chatting system.

---

## Tech Stack

1. Node.js  
2. Built-in package: `http`  
3. External package: `websocket`

---

## Basic Functionality

Enables real-time message pushing by using WebSocket to simulate receiving messages inside a chat.

---

## How to Use It

### 1. Install Dependencies

Install the necessary packages by running the following command in your console:

```bash
npm i
```

---

### 2. Prepare Your Terminal

You will need to split your terminal window so you have **two separate console prompts**.

---

### 3. Enter Node REPL Mode

In each terminal, enter Node REPL mode by running:

```bash
node
```

---

### 4. Create a WebSocket Connection

Once in REPL mode, insert the following code into your terminal:

```js
let ws = new WebSocket("ws://localhost:8080")
```

You can perform this step in one terminal at a time or both at once.

After inserting this command, you should see an `undefined` message on the next line. If not, double-check that the code was copied correctly.

---

### 5. Start Listening for Messages

To listen to the conversation in real time, insert the following code into your terminal:

```js
ws.onmessage = message => console.log(`${message.data}`)
```

Repeat this step in the second terminal if you haven’t done so already.

At this point, if nothing went wrong, you should not see any errors. If that’s the case, great job.

---

### 6. Send Messages

Use the following command to start chatting. This command sends a message to the chat:

```js
ws.send("Your message here..")
```

---

## How It Works (Deeper Detail)

After importing `http` and `websocket`, an HTTP server instance is created. This HTTP server is passed as an argument to the WebSocket instance so it can operate on the same port as the HTTP server.

An empty array called `connections` is created to store all currently connected users.

Next, actions are defined for specific events:

- When the WebSocket receives a `request`, it creates a new connected user instance. This instance takes two parameters: `AcceptedProtocol` and `AllowedOrigin`. The value `request.origin` is used to track where the request came from.

- When a connection receives a `message`, that message is sent to every other connection (user). The value `connection.socket.remotePort` is used as a unique identifier to assign each user an appropriate ID.

- In the final step, the new connection (user) is pushed into the `connections` array, and a message announcing the new connection is sent to every other user.

