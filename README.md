# Peer-to-Peer Networking Made Easy Using Hyperswarm

## Table of Contents

- [Introduction](#introduction)
- [About Hyperswarm](#about-hyperswarm)
- [Requirements](#requirements)
- [Integrate Dependencies](#integrate-dependencies)
- [Development](#development)
- [Result](#result)
- [Conclusion](#conclusion)
- [Reference](#reference)

### Introduction

This document provides an in-depth overview of developing a **[peer-to-peer networking](https://www.geeksforgeeks.org/what-is-p2p-peer-to-peer-process/)** tool leveraging **Hyperswarm** in a JavaScript environment, specifically focusing on integrating it with an Express.js server.

### About Hyperswarm

[Hyperswarm](https://docs.holepunch.to/building-blocks/hyperswarm) simplifies peer discovery and connection for shared interests over a distributed network, often using Hypercore's **discovery key as the topic**. It is a networking tool that excels in establishing secure, direct connections between peers, bypassing NAT traversal complexities.

### Requirements

1. Any operating system (MacOS, Linux, and Windows).
2. A laptop or desktop with [Node.js installed](https://nodejs.org/en) (LTS Version preferred - Node v16 or greater).
3. [VS Code](https://code.visualstudio.com/download) or any other [open source code editor](https://www.hostinger.in/tutorials/best-code-editors).
4. Stable internet connection.

### Integrate Dependencies

1. **Node.js and npm Installation**: Install Node.js, which includes npm, the package manager for Node.js. Node.js provides the runtime environment, while [npm manages project dependencies](https://www.w3schools.com/whatis/whatis_npm.asp).
2. **Initializing the Project**: Use `npm init` in the project directory. This command initializes a new Node.js project by creating a `package.json` file, which will track project dependencies and metadata.
    - Create a Project Folder: Make a new directory for the project.
    - Initialize Node.js Project: Inside the project directory using the terminal, run `npm init` to create a `package.json` file.

      ![Project Initialization](markdown/10.PNG)
     
      Once it’s done, `package.json` should be visible in the explorer section under the project folder.

3. **Installing Hyperswarm**: Execute `npm install hyperswarm` in the terminal window to add Hyperswarm to the project. Hyperswarm enables the creation of a distributed, peer-to-peer network, allowing the application to find and connect to peers sharing a common topic.

    ```javascript
    npm install hyperswarm
    ```

4. Further use of other Holepunch’s [building blocks](https://docs.holepunch.to/quick-start) for networking:

    ```javascript
    npm install hyperswarm hypercore corestore hyperbee hyperdrive localdrive b4a debounceify graceful-goodbye --save
    ```

5. Ensure all dependencies are installed properly.

### Development

#### Step 1: Setting Up the Server (`server.js`)

1. **Initialize Express and Hyperswarm:**
    ```javascript
    const express = require('express');
    const Hyperswarm = require('hyperswarm');
    const app = express();
    const swarm = new Hyperswarm();
    ```

2. **Configure Express Routes:**
    ```javascript
    // Express routes
    app.get('/', (req, res) => {
      res.send('Hello World from Express!');
    });
    ```

3. **Start the Express Server:**
    ```javascript
    // Start Express server
    app.listen(port, () => {
      console.log(`Express server listening at http://localhost:${port}`);
    });
    ```

4. **Setup Hyperswarm Connection:**
    ```javascript
    // Join a topic
    const topic = crypto.createHash('sha256').update('Namaste').digest();
    swarm.join(topic, {
      lookup: true,
      announce: true
    });
    ```

5. **Handle Hyperswarm Connections:**
    ```javascript
    swarm.on('connection', (conn) => { /* Connection handling code */ });
    ```

    Example for handling code:
    ```javascript
    swarm.on('connection', (conn) => {
      console.log('New hyperswarm connection!');
      conn.on('data', (data) => {
        console.log('Received data:', data.toString());
      });
      conn.write('Hello, peer!');
    });
    ```

#### Step 2: Setting Up the Client (`client.js`)

1. **Hyperswarm Client Configuration:**
    ```javascript
    const Hyperswarm = require('hyperswarm');
    const swarm = new Hyperswarm();
    swarm.join(Buffer.from('Namaste'), { lookup: true });
    ```

2. **Handle Connections:**
    ```javascript
    swarm.on('connection', (socket) => { /* Connection handling code */ });
    ```

    Example for handling code:
    ```javascript
    swarm.on('connection', (socket, details) => {
      console.log('Connected to the server!', details);

      // You can read data from the socket or write data to the socket
      socket.on('data', (data) => {
        console.log('Received data:', data.toString());
      });
    });
    ```

#### Step 3: Testing and Debugging

1. Running the Server: Start the server with `node server.js` and check for console logs.
2. Running the Client: Execute the client with `node client.js`.
3. Debugging: Monitor connections and data exchange; troubleshoot any issues that arise.

### Result

Overview of successful implementation: The server correctly announces its presence on the Hyperswarm network, and the client connects and exchanges data, demonstrating a functional peer-to-peer network.

1. **Server Actively Started Listening:**

    ![Server Listening](markdown/final_6.PNG)

2. **Client Connected to the Server:**

    ![Client Connected](markdown/final_2.PNG)

3. **Exchange of Messages:**

    Client Side:

    ![Client Side Message](markdown/final_4.PNG)

    Server Side:

    ![Server Side Message](markdown/final_5.PNG)

### Conclusion

Reflects on the project's success in demonstrating the capabilities of Hyperswarm in creating decentralized applications, and potential future enhancements or use cases in peer-to-peer networking.

### Reference

- [Holepunch Documentation](https://docs.holepunch.to/)
- [Hyperswarm Documentation](https://github.com/hyperswarm/hyperswarm)
- [Express.js Documentation](https://expressjs.com/)
