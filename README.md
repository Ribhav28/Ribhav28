# 🌐 Exposing local server using Hyperswarm-DHT & Hypertele

### Requirements 📋

> 1. A laptop or desktop with [Node.js installed](https://nodejs.org/en) (LTS Version preferred - Node v16 or greater).
> 2. [VS Code](https://code.visualstudio.com/download) or any other [open source code editor](https://www.hostinger.in/tutorials/best-code-editors).

## Table of Contents 📚

- [Introduction](#introduction)
- [Integrate Dependencies](#integrate-dependencies)
- [Development](#development)
- [Result](#result)
- [Reference](#reference)

### Introduction

This document provides an in-depth overview of developing a **[peer-to-peer networking](https://www.geeksforgeeks.org/what-is-p2p-peer-to-peer-process/)** tool leveraging **[Hyperswarm](https://docs.holepunch.to/building-blocks/hyperswarm)** and **[Hypertele](https://docs.holepunch.to/tools/hypertele)**, specifically focusing on integrating it with an Express.js server. The main purpose is for the client to listen on a local port on one laptop through which it can access the server running on another laptop, which is an express server. It should also proxy the traffic to the webserver.

### Integrate Dependencies

1. **Installing Hyperswarm**: 
    ```shell
    npm install hyperswarm
    ```
2. **Installing [Express](https://expressjs.com/en/starter/installing.html)**: 
    ```shell
    npm install express –g
    ```
3. **Installing Hypertele**: 
    ```shell
    npm install -g hypertele
    ```
4. Ensure all dependencies are installed properly.

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
    const port = 3000;
    app.listen(port, () => {
      console.log(`Express server listening at http://localhost:${port}`);
    });
    ```

4. **Setup Hyperswarm Connection:**
    ```javascript
    const crypto = require('crypto');
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

#### Step 2: Generate seed for Hypertele Server:
    
    const crypto = require('crypto');
    // Your chosen seed phrase
    const seedPhrase = 'Namaste'; // Use your phrase
    const seed = crypto.createHash('sha256').update(seedPhrase).digest('hex');
    console.log(seed);
  
    
7. Use these commands to print key using generated seed value & further use the printed key to help client get remote access:
    ```shell
    hypertele-server --seed <Generated_Seed> -l <Local Port> // Server
    hypertele -s <Printed_Key> -p <Local Port> // Client
    ```

### Result

Voilà! The client is able to access the Express server remotely. 🍐

### Reference

- [Holepunch Documentation](https://docs.holepunch.to/)
- [Hyperswarm Documentation](https://github.com/hyperswarm/hyperswarm)
- [Express.js Documentation](https://expressjs.com/)
- [Hypertele Documentation](https://docs.holepunch.to/tools/hypertele)
