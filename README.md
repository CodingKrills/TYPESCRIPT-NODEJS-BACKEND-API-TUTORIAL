
# How to Create a Simple REST API using TypeScript and Node.js

A brief description of what this project does and who it's for

Typescript is a superset of JavaScript with additional features such as static types checking. Typescript is gaining a lot of popularity among JavaScript developers. It is a fast-developing programming language for building extensive applications.

resource :- https://www.section.io/engineering-education/how-to-create-a-simple-rest-api-using-typescript-and-nodejs/

### Prerequisites

- Ensure that you have Node.js and Postman installed on your machine.
- Ensure you have essential experience of how to write and execute Typescript.
- Be familiar with Node.js and how to use libraries such as Express.js.
- Be familiar with how to test APIs using Postman (a tool for interacting with web-based APIs).

### Installing Typescript

Unlike JavaScript, Typescript doesn’t run directly on the browser. To execute any Typescript written code, you need a Typescript compiler.

This will compile Typescript into JavaScript. This way, it will be easier to execute and run the Typescripts on a browser. Since we are using Node.js, we will install Typescript from NPM using the command below.

``` 
npm install -g typescript 

```
Adding the –g flag to install the packages globally ensures that Typescript is available to any Node.js project.

### Initialize Node.js

To start a Node.js project, create a project folder and run npm init. Follow the prompts. This will create a package.json file that will save any installed dependencies for your project.

```sh
Alternatively, run npm init -y to auto-generate the package.json file.

```

### Install project dependencies

In this application, we are going to use the following Node.js libraries.

- TypeScript: A TypeScript compiler with static set type definitions.
- Ts-node: Allows us to run and configure Typescript execution environments.
- Express: Node.js web application framework for setting and managing web-based server.
- @types/express: Type definitions for Express.
- Morgan: A Node.js HTTP request logger middleware for Node.js.
- @types/morgan: Type definitions for Morgan.
- Axios: A Node.js promise-based HTTP client library for Node.js, for sending HTTP requests to query and consume resources from APIs.
- @types/Axios: Type definitions for Axios.
- Nodemon: A server utility library for monitoring changes of the code on a text editor. It automatically restarts the server whenever code changes are detected.

To install all these libraries, run the following command.

```
npm install typescript ts-node express @types/express morgan @types/morgan axios @types/axios nodemon

```

### Initialize Typescript

To execute Typescript with Node.js, you need the tsconfig.json file. This file sets all the environments required to run Typescript. You can create the file manually or run tsc --init to generate a sample tsconfig.json file at the root of your project.

### Setting up the tsconfig.json

Make sure your file look like this.

```
{
    "compilerOptions": {
        "forceConsistentCasingInFileNames": true,
        "module": "commonjs",
        "esModuleInterop": true,
        "outDir": "./build",
        "rootDir": "./source",
        "target": "es6",
        "skipLibCheck": true,
        "strict": true
    }
}

```

Check out this documentation to learn more about the tsconfig.json.

### Modify package.json

Head over to your project package.json file and modify the main and scripts with the following values.

```

"main": "source/server.ts",
"scripts": {
    "dev": "nodemon source/server.ts",
    "build": "rm -rf build/ && prettier --write source/ && tsc"
}

```
This will set up the command to build and compile the .ts file to the .js file. In this case, we can then start the development server using the command npm run dev.

### Setting up the application structure

Your project files and subfolders should be set up as shown below.

```
|   package-lock.json
|   package.json
|   tsconfig.json
\---source
    |   server.ts
    \---controllers
    |       posts.ts
    \---routes
            posts.ts

```

Create the source folder inside your project directory. The source folder will include all the .ts files the application needs to run, as explained earlier.

### Setting up the controllers

Create the controllers folder. In it have the posts.ts file. This module will handle all the API logic, i.e. getting posts, getting a single post, updating a post, deleting a post, and creating a post.

```
controllers/posts.ts
```

```
/** source/controllers/posts.ts */
import { Request, Response, NextFunction } from 'express';
import axios, { AxiosResponse } from 'axios';

interface Post {
    userId: Number;
    id: Number;
    title: String;
    body: String;
}

// getting all posts
const getPosts = async (req: Request, res: Response, next: NextFunction) => {
    // get some posts
    let result: AxiosResponse = await axios.get(`https://jsonplaceholder.typicode.com/posts`);
    let posts: [Post] = result.data;
    return res.status(200).json({
        message: posts
    });
};

// getting a single post
const getPost = async (req: Request, res: Response, next: NextFunction) => {
    // get the post id from the req
    let id: string = req.params.id;
    // get the post
    let result: AxiosResponse = await axios.get(`https://jsonplaceholder.typicode.com/posts/${id}`);
    let post: Post = result.data;
    return res.status(200).json({
        message: post
    });
};

// updating a post
const updatePost = async (req: Request, res: Response, next: NextFunction) => {
    // get the post id from the req.params
    let id: string = req.params.id;
    // get the data from req.body
    let title: string = req.body.title ?? null;
    let body: string = req.body.body ?? null;
    // update the post
    let response: AxiosResponse = await axios.put(`https://jsonplaceholder.typicode.com/posts/${id}`, {
        ...(title && { title }),
        ...(body && { body })
    });
    // return response
    return res.status(200).json({
        message: response.data
    });
};

// deleting a post
const deletePost = async (req: Request, res: Response, next: NextFunction) => {
    // get the post id from req.params
    let id: string = req.params.id;
    // delete the post
    let response: AxiosResponse = await axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`);
    // return response
    return res.status(200).json({
        message: 'post deleted successfully'
    });
};

// adding a post
const addPost = async (req: Request, res: Response, next: NextFunction) => {
    // get the data from req.body
    let title: string = req.body.title;
    let body: string = req.body.body;
    // add the post
    let response: AxiosResponse = await axios.post(`https://jsonplaceholder.typicode.com/posts`, {
        title,
        body
    });
    // return response
    return res.status(200).json({
        message: response.data
    });
};

export default { getPosts, getPost, updatePost, deletePost, addPost };
```

We include all the necessary API methods such as:

- getPosts - A request to fetch all posts in the list.
- getPost - A request to fetch a single post by id.
- updatePost - A request to update a post with new values.
- deletePost - A request to delete an existing post.
- addPost - A request to add a new post to the existing list.
