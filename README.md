This is a very basic example of a realtime chatting system

Tech Stack:
1.Node.js, 
2.built-in package "http"
3.external package "websocket"


Basic Functionality:
    Enables a real time message pushing by using websocket to simulate recieving a message inside a chat.


How to use it

1. Install necessary package by writing: "npm i" in your console

## For the nex tstep you will need to split your terminal window to have two separate console prompts!

2. In order to be able to execute necessary commands first "node" in your terminal to enter Node REPL mode

3. Once in REPL mode insert this code into your terminal: "let ws = new WebSocket("ws://localhost:8080")"

## (you can do each step into one terminal at a time or both at once, doesnt matter)

## After you inserted command from stage 3 you should see "undefined" message on the next line, otherwise check if you copied code correctly

4. To start listening to a conversation in real time insert this code into your terminal: "ws.onmessage = message => console.log(`${message.data}`)"

5. Now do the same for the second terminal if you haven't yet!

## At this point if nothing went wrong you should have any errors or issues, if so then, great job!

6. Now use this command to start chatting, this command will send message to the chat: "ws.send("Your message here..")"


How it works in deeper detail

After we import "http" and "websocket" we create an http server instance that websocket instance will take as an argument inside its own instance to work on port of our HTPP server!

We also create an empty array called "connections" to store of our current connected users.

Next step is to establish actions that will happen when certain events occur

When websocket receives a "request" it creates an instance of a connected user that takes 2 parameters (AcceptedProtocol and Allowedorigin), we write "request.origin" to track where the requests came from.

Next when the connection recieves a "message" we send this message to EVERY OTHER CONNECTION AKA a user, notice that we use "connection.socket.remotePort" as a unique identifier in order to give every user appropriate ID.

In the final step we push a new connection aka user to our array of connections and then we send a message about that connection to every other user.