# Node Js Setup with typescript
Node Js Setup
Install and Verify Node js in your Operating System

Go to https://nodejs.org/en and download Node JS

Step 1: Create a project folder
   mkdir nodejs-with-ts
   cd nodejs-with-ts/

Step 2 : Initialise a node js project
   npm init -y

Create a src folder in the root and in it create index.ts file

console.log(2 + 3);

Step 3 : Install Typescript with Types
    npm i -D typescript @types/node

Verify the Installation by running

    npx tsc -v

Step 4 : Create Typescript config file
    npx tsc --init

Modify the generated tsconfig file to this

{
  "compilerOptions": {
    "module": "CommonJS",
    "target": "ES2016",
    "noImplicitAny": true,
    "removeComments": true,
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "rootDir": "./src",
    "outDir": "./dist",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
 

Step 5 : Install Other Packages we use in Project
Install express

    npm install express @types/express

Install dotenv and cors

    npm install cors dotenv

cors: Middleware for enabling Cross-Origin Resource Sharing (CORS) in your application. It allows your server to handle requests from different origins (domains, ports, or protocols), which is essential for accessing resources from a web browser when your frontend and backend are hosted on different domains.

dotenv: A module that loads environment variables from a .env file into process.env. It's used to manage sensitive configuration data such as API keys, database connection strings, and other environment-specific settings without hardcoding them in your source code.

Install Bycrpt and its types

    npm install bcrypt @types/bcrypt

# Install Prisma and Prisma Client
    npm install prisma @prisma/client

    Initialize Prisma
    npx prisma init --datasource-provider dbname

prisma: This is the Prisma CLI, which is used to manage your Prisma schema, generate the Prisma Client, and run database migrations. It's essential for setting up and managing your database schema with Prisma.

@prisma/client: This is the auto-generated database client that is tailored to your Prisma schema. It provides a strongly-typed, intuitive API for interacting with your database, making it easy to query and manipulate data with TypeScript support.

Install Build Tools

   npm install --save-dev tsc-alias ts-node-dev tsconfig-paths

** tsc-alias **: A tool that replaces path aliases in compiled JavaScript files after the TypeScript compiler (tsc) runs. It allows you to use path aliases (e.g., @/components) defined in tsconfig.json in your TypeScript code and ensures they are correctly resolved in the output files.

** ts-node-dev **: A development tool that automatically restarts your Node.js application when file changes are detected. It is similar to nodemon but optimized for TypeScript. It also provides faster restarts by using ts-node for on-the-fly TypeScript compilation and caching the results.

** tsconfig-paths **: A package that enables Node.js to recognize and resolve path aliases defined in your tsconfig.json when running TypeScript directly (e.g., with ts-node or ts-node-dev). This ensures that modules can be imported using the defined aliases instead of relative paths.

Step 6 : Modify the Script in your package.json file
"scripts": {
    "dev": "tsnd --respawn -r tsconfig-paths/register --pretty --transpile-only ./src/index.ts",
    "build": "tsc && tsc-alias",
    "start": "node ./dist",
    "postinstall": "prisma generate"
  },

Step 7 : Project File Structure
Step 8 : Create an express server
Modify your src/index.ts to this

import express from "express"; // Import the Express framework
 
require("dotenv").config(); // Load environment variables from a .env file into process.env
const cors = require("cors"); // Import the CORS middleware
const app = express(); // Create an Express application instance
 
app.use(cors()); // Enable Cross-Origin Resource Sharing (CORS) for all routes
 
const PORT = process.env.PORT || 8000; // Set the server's port from environment variables or default to 8000
 
app.use(express.json()); // Parse incoming JSON requests and make the data available in req.body
 
app.listen(PORT, () => {
  // Start the server and listen on the specified port
  console.log(`Server is running on http://localhost:${PORT}`); // Log a message indicating the server is running
});

Summary of What the Code Does:

Express Setup: The code sets up an Express server, a popular Node.js framework for building web applications and APIs.

Environment Variables: The dotenv package is used to load environment variables from a .env file, making them accessible via process.env.

CORS Middleware: The cors middleware is used to enable Cross-Origin Resource Sharing, which allows the server to handle requests from different domains.

Port Configuration: The server's port is set based on the PORT environment variable, or it defaults to 8000 if not specified.

JSON Parsing: The express.json() middleware is used to automatically parse incoming JSON payloads and make them available in req.body.

Server Start: The server is started by calling app.listen(), and it listens for incoming requests on the specified port, logging a message once it is running.

Step 9 Create a simple API Enpoint
import express, { Request, Response } from "express";
// GET REQUEST
app.get("/customers", (req: Request, res: Response) => {
  const customers = [
    { name: "John Doe", email: "john.doe@example.com", phone: "+1234567890" },
    {
      name: "Joel Smith",
      email: "joel.smith@example.com",
      phone: "+0987654321",
    },
  ];
 
  return res.status(200).json(customers);
});
