# Share the application

Now that you’ve built an image, you can share it. To share Docker images, you have to use a Docker registry. The default registry is Docker Hub and is where all of the images you’ve used have come from.

A Docker ID allows you to access Docker Hub which is the world’s largest library and community for container images.

## Create a repo

To push an image, you first need to create a repository on Docker Hub.

- Sign up or Sign in to Docker Hub.
- Select the Create Repository button.
- For the repo name, use getting-started. Make sure the Visibility is Public.
- Select the Create button.

If you look at the image below an example Docker command can be seen. This command will push to this repo.

[Docker Hub Push image](https://docs.docker.com/get-started/images/push-command.png)

## Push the image

In the command line, try running the push command you see on Docker Hub. Note that your command will be using your namespace, not “docker”.

```
docker push docker/getting-started
 The push refers to repository [docker.io/docker/getting-started]
 An image does not exist locally with the tag: docker/getting-started
```

Why did it fail? The push command was looking for an image named docker/getting-started, but didn’t find one. If you run docker image ls, you won’t see one either.

To fix this, you need to “tag” your existing image you’ve built to give it another name.

- Login to the Docker Hub using the command docker login -u YOUR-USER-NAME.
- Use the docker tag command to give the getting-started image a new name. Be sure to swap out YOUR-USER-NAME with your Docker ID.

```
docker tag getting-started YOUR-USER-NAME/getting-started
```

Now try your push command again. If you’re copying the value from Docker Hub, you can drop the tagname portion, as you didn’t add a tag to the image name. If you don’t specify a tag, Docker will use a tag called latest.

```
docker push YOUR-USER-NAME/getting-started
```

## Run the image on a new instance

Now that your image has been built and pushed into a registry, try running your app on a brand new instance that has never seen this container image. To do this, you will use Play with Docker.

- Open your browser to Play with Docker.
- Select Login and then select docker from the drop-down list.
- Connect with your Docker Hub account.
- Once you’re logged in, select the ADD NEW INSTANCE option on the left side bar. If you don’t see it, make your browser a little wider. After a few seconds, a terminal window opens in your browser.
- In the terminal, start your freshly pushed app.

```
docker run -dp 0.0.0.0:3000:3000 YOUR-USER-NAME/getting-started
```

You should see the image get pulled down and eventually start up.

You may have noticed that this command binds the port mapping to a different IP address. Previous docker run commands published ports to 127.0.0.1:3000 on the host. This time, you’re using 0.0.0.0.

Binding to 127.0.0.1 only exposes a container’s ports to the loopback interface. Binding to 0.0.0.0, however, exposes the container’s port on all interfaces of the host, making it available to the outside world.

- Select on the 3000 badge when it comes up and you should see the app with your modifications. If the 3000 badge doesn’t show up, you can select on the Open Port button and type in 3000.
