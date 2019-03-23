## Create the Node.js app

First, create a new directory where all the files would live.
In this directory create a package.json file that describes your app and its dependencies:

```
{
  "name": "docker_web_app",
  "version": "1.0.0",
  "description": "Node.js on Docker",
  "author": "First Last <first.last@example.com>",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.16.1"
  }
}
```
With your new package.json file, run npm install.<br/>
This will generate a package-lock.json file which will be copied to your Docker image. <br/>

Then, create a server.js file that defines a web app using the Express.js framework:

```
'use strict';

const express = require('express');

// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello world\n');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```

## Create a Dockerfile

Create the dockerfile and copy the contents from the Dockerfile here.<br/>

Your app binds to port 8080 so you'll use the EXPOSE instruction to have it<br/>
mapped by the docker daemon:

```
EXPOSE 8080
```

Last but not least, define the command to run your app using CMD which defines your runtime.<br/>
Here we will use the basic npm start which will run node server.js to start your server:

```
CMD [ "npm", "start" ]
```

## .dockerignore file

Create a .dockerignore file in the same directory as your Dockerfile with following content:
```
node_modules
npm-debug.log
```

This will prevent your local modules and debug logs from being copied onto your Docker image and possibly overwriting modules installed within your image.

## Building your image
Go to the directory that has your Dockerfile and run the following command to build the Docker image. The -t flag lets you tag your image so it's easier to find later using the docker images command:

```
$ docker build -t <your_username>/node-web-app .
```
Install docker on your system and signup. Replace <your_username> with your username.


Your image will now be listed by Docker:

$ docker images

```

# Example
REPOSITORY                      TAG        ID              CREATED
node                            8          1934b0b038d1    5 days ago
<your username>/node-web-app    latest     d64d3505b0d2    1 minute ago
```
