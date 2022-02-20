
## Steps 

### Installing Typescript

Unlike JavaScript, Typescript doesn’t run directly on the browser. To execute any Typescript written code, you need a Typescript compiler.

This will compile Typescript into JavaScript. This way, it will be easier to execute and run the Typescripts on a browser. Since we are using Node.js, we will install Typescript from NPM using the command below.

npm install -g typescript

Adding the –g flag to install the packages globally ensures that Typescript is available to any Node.js project

###  Initialize Node.js

To start a Node.js project, create a project folder and run npm init. Follow the prompts. This will create a package.json file that will save any installed dependencies for your project.

Alternatively, run npm init -y to auto-generate the package.json file.

### Install project dependencies

In this application, we are going to use the following Node.js libraries.

TypeScript: A TypeScript compiler with static set type definitions.
Ts-node: Allows us to run and configure Typescript execution environments.
Express: Node.js web application framework for setting and managing web-based server.
@types/express: Type definitions for Express.
Morgan: A Node.js HTTP request logger middleware for Node.js.
@types/morgan: Type definitions for Morgan.
Axios: A Node.js promise-based HTTP client library for Node.js, for sending HTTP requests to query and consume resources from APIs.
@types/Axios: Type definitions for Axios.
Nodemon: A server utility library for monitoring changes of the code on a text editor. It automatically restarts the server whenever code changes are detected.
To install all these libraries, run the following command.

npm install typescript ts-node express @types/express morgan @types/morgan axios @types/axios nodemon