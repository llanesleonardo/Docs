# Docker NodeJS

The Node.js getting started guide teaches you how to create a containerized Node.js application using Docker. In this guide, you’ll learn how to:

- Create a simple Node.js application
- Create a new Dockerfile which contains instructions required to build a Node.js image
- Run the newly built image as a container
- Set up a local development environment to connect a database to the container
- Use Docker Compose to run the Node.js application
- Configure a CI/CD pipeline for your application using GitHub Actions.

After completing the Node.js getting started modules, you should be able to containerize your own Node.js application based on the examples and instructions provided in this guide.

## Prerequisites

- You understand basic Docker concepts.
- You’re familiar with the Dockerfile format.
- You have enabled BuildKit on your machine.

## Overview

Now that we have a good overview of containers and the Docker platform, let’s take a look at building our first image. An image includes everything you need to run an application - the code or binary, runtime, dependencies, and any other file system objects required.

To complete this tutorial, you need the following:

- Node.js version 18 or later. Download Node.js
- Docker running locally: Follow the instructions to download and install Docker.
- An IDE or a text editor to edit files. We recommend using Visual Studio Code

## Sample application

Let’s create a simple Node.js application that we can use as our example. Create a directory in your local machine named node-docker and follow the steps below to create a simple REST API.

```
cd [path to your node-docker directory]
npm init -y
npm install ronin-server ronin-mocks
touch server.js
```

Now, let’s add some code to handle our REST requests. We’ll use a mock server so we can focus on Dockerizing the application.

Open this working directory in your IDE and add the following code into the server.js file.

```
const ronin = require('ronin-server')
const mocks = require('ronin-mocks')

const server = ronin.server()

server.use('/', mocks.server(server.Router(), false, true))
server.start()
```

The mocking server is called Ronin.js and will listen on port 8000 by default. You can make POST requests to the root (/) endpoint and any JSON structure you send to the server will be saved in memory. You can also send GET requests to the same endpoint and receive an array of JSON objects that you have previously POSTed.

## Test the application

Let’s start our application and make sure it’s running properly. Open your terminal and navigate to your working directory you created.

```
node server.js
```

To test that the application is working properly, we’ll first POST some JSON to the API and then make a GET request to see that the data has been saved. Open a new terminal and run the following curl commands:

```
curl --request POST \
  --url http://localhost:8000/test \
  --header 'content-type: application/json' \
  --data '{"msg": "testing" }'
{"code":"success","payload":[{"msg":"testing","id":"31f23305-f5d0-4b4f-a16f-6f4c8ec93cf1","createDate":"2020-08-28T21:53:07.157Z"}]}
curl http://localhost:8000/test
{"code":"success","meta":{"total":1,"count":1},"payload":[{"msg":"testing","id":"31f23305-f5d0-4b4f-a16f-6f4c8ec93cf1","createDate":"2020-08-28T21:53:07.157Z"}]}
```

Switch back to the terminal where our server is running. You should now see the following requests in the server logs.

```
2020-XX-31T16:35:08:4260  INFO: POST /test
2020-XX-31T16:35:21:3560  INFO: GET /test
```

Great! We verified that the application works. At this stage, you’ve completed testing the server script locally.

Press CTRL-c from within the terminal session where the server is running to stop it.

```
2021-08-06T12:11:33:8930  INFO: POST /test
2021-08-06T12:11:41:5860  INFO: GET /test
^Cshutting down...
```

We will now continue to build and run the application in Docker.

## Create a Dockerfile for Node.js

Next, we need to add a line in our Dockerfile that tells Docker what base image we would like to use for our application.

```
# syntax=docker/dockerfile:1

FROM node:18-alpine
```

Docker images can be inherited from other images. Therefore, instead of creating our own base image, we’ll use the official Node.js image that already has all the tools and packages that we need to run a Node.js application. You can think of this in the same way you would think about class inheritance in object oriented programming. For example, if we were able to create Docker images in JavaScript, we might write something like the following.

```
class MyImage extends NodeBaseImage {}

```

This would create a class called MyImage that inherited functionality from the base class NodeBaseImage.

In the same way, when we use the FROM command, we tell Docker to include in our image all the functionality from the node:18-alpine image.

The NODE_ENV environment variable specifies the environment in which an application is running (usually, development or production). One of the simplest things you can do to improve performance is to set NODE_ENV to production.

```
ENV NODE_ENV=production
```

To make things easier when running the rest of our commands, let’s create a working directory. This instructs Docker to use this path as the default location for all subsequent commands. This way we do not have to type out full file paths but can use relative paths based on the working directory.

```
WORKDIR /app
```

Usually the very first thing you do once you’ve downloaded a project written in Node.js is to install npm packages. This ensures that your application has all its dependencies installed into the node_modules directory where the Node runtime will be able to find them.

Before we can run npm install, we need to get our package.json and package-lock.json files into our images. We use the COPY command to do this. The COPY command takes two parameters: src and dest. The first parameter src tells Docker what file(s) you would like to copy into the image. The second parameter dest tells Docker where you want that file(s) to be copied to. For example:

```
COPY ["<src>", "<dest>"]
```

You can specify multiple src resources seperated by a comma. For example, COPY ["<src1>", "<src2>",..., "<dest>"]. We’ll copy the package.json and the package-lock.json file into our working directory /app.

```
COPY ["package.json", "package-lock.json*", "./"]
```

Note that, rather than copying the entire working directory, we are only copying the package.json file. This allows us to take advantage of cached Docker layers. Once we have our files inside the image, we can use the RUN command to execute the command npm install. This works exactly the same as if we were running npm install locally on our machine, but this time these Node modules will be installed into the node_modules directory inside our image.

```
RUN npm install --production
```

At this point, we have an image that is based on node version 18 and we have installed our dependencies. The next thing we need to do is to add our source code into the image. We’ll use the COPY command just like we did with our package.json files above.

```
COPY . .
```

The COPY command takes all the files located in the current directory and copies them into the image. Now, all we have to do is to tell Docker what command we want to run when our image is run inside of a container. We do this with the CMD command.

```
CMD ["node", "server.js"]
```

Here’s the complete Dockerfile.

```
# syntax=docker/dockerfile:1

FROM node:18-alpine
ENV NODE_ENV=production

WORKDIR /app

COPY ["package.json", "package-lock.json*", "./"]

RUN npm install --production

COPY . .

CMD ["node", "server.js"]
```

## Create a .dockerignore file

To use a file in the build context, the Dockerfile refers to the file specified in an instruction, for example, a COPY instruction. A .dockerignore file lets you specify files and directories to be excluded from the build context. To improve the build’s performance, create a .dockerignore file and add the node_modules directory in it:

```
node_modules
```

## Build image

Now that we’ve created our Dockerfile, let’s build our image. To do this, we use the docker build command. The docker build command builds Docker images from a Dockerfile and a “context”. A build’s context is the set of files located in the specified PATH or URL. The Docker build process can access any of the files located in the context.

The build command optionally takes a --tag flag. The tag is used to set the name of the image and an optional tag in the format ‘name:tag’. We’ll leave off the optional “tag” for now to help simplify things. If you do not pass a tag, Docker will use “latest” as its default tag. You’ll see this in the last line of the build output.

Let’s build our first Docker image.

```
docker build --tag node-docker .

[+] Building 93.8s (11/11) FINISHED
 => [internal] load build definition from dockerfile                                          0.1s
 => => transferring dockerfile: 617B                                                          0.0s
 => [internal] load .dockerignore                                                             0.0s
 ...
 => [2/5] WORKDIR /app                                                                        0.4s
 => [3/5] COPY [package.json, package-lock.json*, ./]                                         0.2s
 => [4/5] RUN npm install --production                                                        9.8s
 => [5/5] COPY . .
```

## View local images

To see a list of images we have on our local machine, we have two options. One is to use the CLI and the other is to use Docker Desktop. Since we are currently working in the terminal let’s take a look at listing images with the CLI.

To list images, simply run the images command.

```
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
node-docker         latest              3809733582bc        About a minute ago   945MB
```

Your exact output may vary, but you should see the image we just built node-docker:latest with the latest tag.

## Tag images

An image name is made up of slash-separated name components. Name components may contain lowercase letters, digits and separators. A separator is defined as a period, one or two underscores, or one or more dashes. A name component may not start or end with a separator.

An image is made up of a manifest and a list of layers. In simple terms, a “tag” points to a combination of these artifacts. You can have multiple tags for an image. Let’s create a second tag for the image we built and take a look at its layers.

To create a new tag for the image we built above, run the following command.

```
docker tag node-docker:latest node-docker:v1.0.0
```

The Docker tag command creates a new tag for an image. It does not create a new image. The tag points to the same image and is just another way to reference the image.

Now run the docker images command to see a list of our local images.

```
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
node-docker         latest              3809733582bc        24 minutes ago      945MB
node-docker         v1.0.0              3809733582bc        24 minutes ago      945MB
```

You can see that we have two images that start with node-docker. We know they are the same image because if you look at the IMAGE ID column, you can see that the values are the same for the two images.

Let’s remove the tag that we just created. To do this, we’ll use the rmi command. The rmi command stands for “remove image”.

```
docker rmi node-docker:v1.0.0
Untagged: node-docker:v1.0.0
```

Notice that the response from Docker tells us that the image has not been removed but only “untagged”. Verify this by running the images command.

```
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
node-docker         latest              3809733582bc        32 minutes ago      945MB
```

Our image that was tagged with :v1.0.0 has been removed but we still have the node-docker:latest tag available on our machine.

[Best practices to containerize nodejs web apps](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/)
