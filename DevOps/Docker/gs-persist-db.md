# Persist the DB

In case you didn’t notice, your todo list is empty every single time you launch the container. Why is this? In this part, you’ll dive into how the container is working.

## The container’s filesystem

When a container runs, it uses the various layers from an image for its filesystem. Each container also gets its own “scratch space” to create/update/remove files. Any changes won’t be seen in another container, even if they’re using the same image.

To see this in action, you’re going to start two containers and create a file in each. What you’ll see is that the files created in one container aren’t available in another.

- Start an ubuntu container that will create a file named /data.txt with a random number between 1 and 10000.

```
 docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null" (know more abou at the end of the page)t
```

In case you’re curious about the command, you’re starting a bash shell and invoking two commands (why you have the &&). The first portion picks a single random number and writes it to /data.txt. The second command is simply watching a file to keep the container running.

- Validate that you can see the output by accessing the terminal in the container. To do so, you can use the CLI or Docker Desktop’s graphical interface.

On the command line, use the docker exec command to access the container. You need to get the container’s ID (use docker ps to get it). In your Mac or Linux terminal, or in Windows Command Prompt or PowerShell, get the content with the following command.

```
 docker exec <container-id> cat /data.txt
```

You should see a random number.

- Now, start another ubuntu container (the same image) and you’ll see you don’t have the same file. In your Mac or Linux terminal, or in Windows Command Prompt or PowerShell, get the content with the following command.

```
docker run -it ubuntu ls /
```

In this case the command lists the files in the root directory of the container. Look, there’s no data.txt file there! That’s because it was written to the scratch space for only the first container.

- Go ahead and remove the first container using the docker rm -f <container-id> command.

## Container volumes

With the previous experiment, you saw that each container starts from the image definition each time it starts. While containers can create, update, and delete files, those changes are lost when you remove the container and Docker isolates all changes to that container. With volumes, you can change all of this.

Volumes provide the ability to connect specific filesystem paths of the container back to the host machine. If you mount a directory in the container, changes in that directory are also seen on the host machine. If you mount that same directory across container restarts, you’d see the same files.

There are two main types of volumes. You’ll eventually use both, but you’ll start with volume mounts.

## Persist the todo data

By default, the todo app stores its data in a SQLite database at /etc/todos/todo.db in the container’s filesystem. If you’re not familiar with SQLite, no worries! It’s simply a relational database that stores all the data in a single file. While this isn’t the best for large-scale applications, it works for small demos. You’ll learn how to switch this to a different database engine later.

With the database being a single file, if you can persist that file on the host and make it available to the next container, it should be able to pick up where the last one left off. By creating a volume and attaching (often called “mounting”) it to the directory where you stored the data, you can persist the data. As your container writes to the todo.db file, it will persist the data to the host in the volume.

As mentioned, you’re going to use a volume mount. Think of a volume mount as an opaque bucket of data. Docker fully manages the volume, including the storage location on disk. You only need to remember the name of the volume.

## Create a volume and start the container

You can create the volume and start the container using the CLI or Docker Desktop’s graphical interface.

- Create a volume by using the docker volume create command.

```
docker volume create todo-db

```

- Stop and remove the todo app container once again with docker rm -f <id>, as it is still running without using the persistent volume.

- Start the todo app container, but add the --mount option to specify a volume mount. Give the volume a name, and mount it to /etc/todos in the container, which captures all files created at the path. In your Mac or Linux terminal, or in Windows Command Prompt or PowerShell, run the following command:

```
docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started
```

## Verify that the data persists

- Once the container starts up, open the app and add a few items to your todo list.
- Stop and remove the container for the todo app. Use Docker Desktop or docker ps to get the ID and then docker rm -f <id> to remove it.
- Start a new container using the same steps from above.
- Open the app. You should see your items still in your list.
- Go ahead and remove the container when you’re done checking out your list.

You’ve now learned how to persist data.

## Dive into the volume

A lot of people frequently ask “Where is Docker storing my data when I use a volume?” If you want to know, you can use the docker volume inspect command.

```
docker volume inspect todo-db
[
    {
        "CreatedAt": "2019-09-26T02:18:36Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```

The Mountpoint is the actual location of the data on the disk. Note that on most machines, you will need to have root access to access this directory from the host. But, that’s where it is.

## Bash shell Commands definitions

```
The portion of code you provided ("-c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"") is a command that can be executed in a Bash shell. Let's break it down step by step:

-c: This option is used to specify a command or script to be executed in the shell.

"shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null": This is the command that will be executed.

shuf: It is a command-line utility in Unix-like operating systems that generates random permutations of its input. In this case, it will generate a random number between 1 and 10,000.

-i 1-10000: This option specifies the range of numbers from which shuf should generate a random number. In this case, it is generating a random number between 1 and 10,000.

-n 1: This option tells shuf to generate only one random number.

-o /data.txt: This option specifies the output file where the generated random number will be written. In this case, it will be written to a file named "data.txt" located in the root directory ("/").

&&: This is the logical "AND" operator in Bash. It allows you to execute multiple commands sequentially, where the next command is executed only if the previous command succeeds.

tail -f /dev/null: This command continuously outputs the last 10 lines of a file (tail) and the -f option follows the file as it grows. In this case, /dev/null is a special file that discards anything written to it. This command essentially keeps the shell running indefinitely without displaying any output.

So, when this code is executed in a Bash shell, it will generate a random number between 1 and 10,000, write it to a file named "data.txt," and then the shell will continue running without any visible output.
```
