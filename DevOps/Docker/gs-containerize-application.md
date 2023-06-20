# Containerize and application

For the rest of this guide, you’ll be working with a simple todo list manager that runs on Node.js. If you’re not familiar with Node.js, don’t worry. This guide doesn’t require any prior experience with JavaScript.

To complete this guide, you’ll need the following:

- Docker running locally. Follow the instructions to download and install Docker.
- A Git client.
- If you use Windows and want to use Git Bash to run Docker commands, see Working with Git Bash for syntax differences.
- An IDE or a text editor to edit files. Docker recommends using Visual Studio Code.
- A conceptual understanding of containers and images.

## Get the app

Before you can run the application, you need to get the application source code onto your machine.

- Clone the getting-started repository using the following command:

```
git clone https://github.com/docker/getting-started.git
```

- View the contents of the cloned repository. Inside the getting-started/app directory you should see package.json and two subdirectories (src and spec).

[app image directory](https://docs.docker.com/get-started/images/ide-screenshot.png)

## Build the app’s container image

To build the container image, you’ll need to use a Dockerfile. A Dockerfile is simply a text-based file with no file extension that contains a script of instructions. Docker uses this script to build a container image.

- In the app directory, the same location as the package.json file, create a file named Dockerfile. You can use the following commands below to create a Dockerfile based on your operating system.

In the terminal, run the following commands listed below.

Change directory to the app directory. Replace /path/to/app with the path to your getting-started/app directory.

```
 cd /path/to/app
```

Create an empty file named Dockerfile.

```
 touch Dockerfile
```

- Using a text editor or code editor, add the following contents to the Dockerfile:

```
# syntax=docker/dockerfile:1

FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```

- Build the container image using the following commands:

In the terminal, change directory to the getting-started/app directory. Replace /path/to/app with the path to your getting-started/app directory.

```
 cd /path/to/app
```

Build the container image.

```
 docker build -t getting-started .
```

The docker build command uses the Dockerfile to build a new container image. You might have noticed that Docker downloaded a lot of “layers”. This is because you instructed the builder that you wanted to start from the node:18-alpine image. But, since you didn’t have that on your machine, Docker needed to download the image.

After Docker downloaded the image, the instructions from the Dockerfile copied in your application and used yarn to install your application’s dependencies. The CMD directive specifies the default command to run when starting a container from this image.

Finally, the -t flag tags your image. Think of this simply as a human-readable name for the final image. Since you named the image getting-started, you can refer to that image when you run a container.

The . at the end of the docker build command tells Docker that it should look for the Dockerfile in the current directory.

## Start an app container

Now that you have an image, you can run the application in a container. To do so, you will use the docker run command.

- Start your container using the docker run command and specify the name of the image you just created:

```
 docker run -dp 127.0.0.1:3000:3000 getting-started
```

- After a few seconds, open your web browser to http://localhost:3000. You should see your app.
- Go ahead and add an item or two and see that it works as you expect. You can mark items as complete and remove them. Your frontend is successfully storing items in the backend.

At this point, you should have a running todo list manager with a few items, all built by you.

If you take a quick look at your containers, you should see at least one container running that is using the getting-started image and on port 3000. To see your containers, you can use the CLI or Docker Desktop’s graphical interface.

Run the following docker ps command in a terminal to list your containers.

```
 docker ps
```

Output similar to the following should appear.

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                      NAMES
df784548666d        getting-started     "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        127.0.0.1:3000->3000/tcp   priceless_mcclintock
```
