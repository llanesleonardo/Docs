# Using Kubernetes for remote development

Teams developing large, cloud-native applications might find themselves in a situation where it’s not possible to run the entire application locally on a development machine. There are several reasons why running an application locally is sometimes not feasible:

- It requires more resources than your local machine can provide
- There are dependencies to cloud services, APIs, or networking configurations that can’t be emulated
- Testing and validating requires large amounts of data or network traffic

Often, this means you need to rely on continuous integration pipelines or staging environments to verify code changes. This introduces a time-consuming and cumbersome workflow where you must commit, push, build, test, and deploy your code in order to see them running.

## Combining local and remote

One solution to this problem is to integrate local services with a remote development cluster. In practice, this means starting a service on your development machine using docker run, and allowing that local service to communicate with the development cluster over the network. The remote development cluster hosts workloads that represent the production environment.

A development environment that lets you combine containers running locally with remote resources helps simplify and speed up the inner loop. There are several tools available, commercial and open-source, that you can use to enable a hybrid local-and-remote development environment.

## Telepresence

Telepresence is an open-source CNCF project that helps you integrate local services with a remote Kubernetes cluster. Telepresence works by running a traffic manager pod in Kubernetes, and Telepresence client daemons on developer workstations. The traffic manager acts as a two-way network proxy that can intercept connections and route traffic between the cluster and containers running on developer machines.

- [Telepresence architecture](https://docs.docker.com/develop/images/telepresence-architecture.png)

You have a few options for how the local containers can integrate with the cluster:

- No intercepts
  The most basic integration involves no intercepts at all. Simply establishing a connection between the container and the cluster. This enables the container to access cluster resources, such as APIs and databases.

- Global intercepts
  You can set up global intercepts for a service. This means all traffic for a service will be re-routed from Kubernetes to your local container.

- Personal intercepts
  The more advanced alternative to global intercepts is personal intercepts. Personal intercepts let you define conditions for when a request should be routed to your local container. The conditions could be anything from only routing requests that include a specific HTTP header, to requests targeting a specific route of an API.

- [Telepresence quickstart](https://www.telepresence.io/docs/latest/quick-start/?utm_source=docker-docs&utm_medium=dockerwebsite&utm_campaign=Docker-TP)

## Docker × Ambassador

Sharing a development cluster with a large team can be both a blessing and a curse. Because your teammates are connected to the cluster, you’re able to see what they’re working on. But they can also accidentally step on your intercepts of shared services. Ambassador Labs, creators of Telepresence, run a subscription platform that helps teams share the cluster. You can identify all the intercepts you have running on a service. Each developer can generate an authenticated preview URL to share during code review.

Docker and Ambassador Labs are working together to make running a hybrid local-remote development environment easy and seamless. You can now connect your Docker ID to Ambassador Cloud to sign in and use Telepresence. To get started:

- Go to the Docker × Ambassador page.
- Sign in using your Docker ID.
- Authorize the Ambassador Cloud app.

This takes you to a step-by-step guide on setting up Telepresence, connecting to a development cluster, and creating intercepts.
