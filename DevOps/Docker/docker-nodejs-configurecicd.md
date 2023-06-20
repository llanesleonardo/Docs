# Configure CI/CD for your application

## Get started with GitHub Actions

This tutorial walks you through the process of setting up and using Docker GitHub Actions for building Docker images, and pushing images to Docker Hub. You will complete the following steps:

- Create a new repository on GitHub.
- Define the GitHub Actions workflow.
- Run the workflow.

To follow this tutorial, you need a Docker ID and a GitHub account.

## Step one: Create the repository

Create a GitHub repository and configure the Docker Hub secrets.

- Create a new GitHub repository using this template repository.
  The repository contains a simple Dockerfile, and nothing else. Feel free to use another repository containing a working Dockerfile if you prefer.

- Open the repository Settings, and go to Secrets and variables > Actions.
- Create a new secret named DOCKERHUB_USERNAME and your Docker ID as value.
- Create a new Personal Access Token (PAT) for Docker Hub. You can name this token clockboxci.
- Add the PAT as a second secret in your GitHub repository, with the name DOCKERHUB_TOKEN.

With your repository created, and secrets configured, you’re now ready for action!

## Step two: Set up the workflow

Set up your GitHub Actions workflow for building and pushing the image to Docker Hub.

- Go to your repository on GitHub and then select the Actions tab.
- Select set up a workflow yourself.
  This takes you to a page for creating a new GitHub actions workflow file in your repository, under .github/workflows/main.yml by default.

- In the editor window, copy and paste the following YAML configuration.

```
name: ci

on:
  push:
    branches:
      - "main"

jobs:
  build:
    runs-on: ubuntu-latest
```

- .
  - name: the name of this workflow.
  - on.push.branches: specifies that this workflow should run on every push event for the branches in the list.
  - jobs: creates a job ID (build) and declares the type of machine that the job should run on.

For more information about the YAML syntax used here, see Workflow syntax for GitHub Actions.

## Step three: Define the workflow steps

Now the essentials: what steps to run, and in what order to run them.

```
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      -
        name: Checkout
        uses: actions/checkout@v3
      -
        name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      -
        name: Build and push
        uses: docker/build-push-action@v4
        with:
          context: .
          file: ./Dockerfile
          push: true
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/clockbox:latest
```

The previous YAML snippet contains a sequence of steps that:

- Checks out the repository on the build machine.
- Signs in to Docker Hub, using the Docker Login action and your Docker Hub credentials.
- Creates a BuildKit builder instance using the Docker Setup Buildx action.
- Builds the container image and pushes it to the Docker Hub repository, using Build and push Docker images.
  The with key lists a number of input parameters that configures the step:
  - context: the build context.
  - file: filepath to the Dockerfile.
  - push: tells the action to upload the image to a registry after building it.
    tags: tags that specify where to push the image.

Add these steps to your workflow file. The full workflow configuration should look as follows:

```
name: ci

on:
  push:
    branches:
      - "main"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      -
        name: Checkout
        uses: actions/checkout@v3
      -
        name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      -
        name: Build and push
        uses: docker/build-push-action@v4
        with:
          context: .
          file: ./Dockerfile
          push: true
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/clockbox:latest
```

## Run the workflow

Save the workflow file and run the job.

- Select Commit changes... and push the changes to the main branch.
  After pushing the commit, the workflow starts automatically.

- Go to the Actions tab. It displays the workflow.
  Selecting the workflow shows you the breakdown of all the steps.

- When the workflow is complete, go to your repositories on Docker Hub.
  If you see the new repository in that list, it means the GitHub Actions successfully pushed the image to Docker Hub!
