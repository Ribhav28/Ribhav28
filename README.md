# 🌐 Exposing local server using Hyperswarm

## Table of Contents 📚

- [Introduction](#introduction-)
- [About Hyperswarm](#about-hyperswarm-)
- [Requirements](#requirements-)
- [Integrate Dependencies](#integrate-dependencies-)
- [Development](#development-)
- [Result](#result-)
- [Reference](#reference-)

### Introduction 🚀

This document provides an in-depth overview of developing a **[peer-to-peer networking](https://www.geeksforgeeks.org/what-is-p2p-peer-to-peer-process/)** tool leveraging **Hyperswarm** in a JavaScript environment, specifically focusing on integrating it with an Express.js server.

### About Hyperswarm 👊

[Hyperswarm](https://docs.holepunch.to/building-blocks/hyperswarm) simplifies peer discovery and connection for shared interests over a distributed network, often using Hypercore's **discovery key as the topic**. It is a networking tool that excels in establishing secure, direct connections between peers, bypassing NAT traversal complexities.

### Requirements 📋

> 1. A laptop or desktop with [Node.js installed](https://nodejs.org/en) (LTS Version preferred - Node v16 or greater).
> 2. [VS Code](https://code.visualstudio.com/download) or any other [open source code editor](https://www.hostinger.in/tutorials/best-code-editors).

### Integrate Dependencies 🔗

1. **Installing Hyperswarm**: Execute `npm install hyperswarm` in the terminal window to add Hyperswarm to the project. Hyperswarm enables the creation of a distributed, peer-to-peer network, allowing the application to find and connect to peers sharing a common topic.

    ```javascript
    npm install hyperswarm
    ```

2. Further use of other Holepunch’s [building blocks](https://docs.holepunch.to/quick-start) for networking:

    ```javascript
    npm install hyperswarm hypercore corestore hyperbee hyperdrive localdrive b4a debounceify graceful-goodbye --save
    ```

3. Ensure all dependencies are installed properly.

### Development 🛠️

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

### Result 🎉

Overview of successful implementation: The server correctly announces its presence on the Hyperswarm network, and the client connects and exchanges data, demonstrating a functional peer-to-peer network.

### Reference 🔗

- [Holepunch Documentation](https://docs.holepunch.to/)
- [Hyperswarm Documentation](https://github.com/hyperswarm/hyperswarm)
- [Express.js Documentation](https://expressjs.com/)

