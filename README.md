# 🌐 Exposing local server using Hypertele

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

This document provides an overview of implementing **[peer-to-peer networking](https://www.geeksforgeeks.org/what-is-p2p-peer-to-peer-process/)**, leveraging **[Hypertele](https://docs.holepunch.to/tools/hypertele)**, specifically focusing on integrating it with an Express.js server. The main purpose is for the client to listen on a local port on one laptop through which it can access the server running on another laptop, which is an express server. It should also proxy the traffic to the webserver.

### Integrate Dependencies

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

1. **Initialize Express:**
    ```javascript
    const express = require('express');
    const app = express();
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


#### Step 2: Generate seed for Hypertele Server (`GenerateSeed.js`):
    
    const crypto = require('crypto');
    // Your chosen seed phrase
    const seedPhrase = 'Namaste'; // Use your phrase
    const seed = crypto.createHash('sha256').update(seedPhrase).digest('hex');
    console.log(seed);
    
  
    
1. Use these commands to print key using generated seed value & further use the printed key to help client get remote access:
    ```shell
    hypertele-server --seed <Generated_Seed> -l <Local Port> // Server
    hypertele -s <Printed_Key> -p <Local Port> // Client
    ```

### Result

Voilà! The client can access the Express server remotely. 🍐

### Reference

- [Holepunch Documentation](https://docs.holepunch.to/)
- [Hyperswarm Documentation](https://github.com/hyperswarm/hyperswarm)
- [Express.js Documentation](https://expressjs.com/)
- [Hypertele Documentation](https://docs.holepunch.to/tools/hypertele)
