Back: [Github Actions](./gha.md)

# Github actions Deployment

You can create custom continuous deployment (CD) workflows directly in your GitHub repository with GitHub Actions.

Continuous deployment (CD) is the practice of using automation to publish and deploy software updates. As part of the typical CD process, the code is automatically built and tested before deployment.

Continuous deployment is often coupled with continuous integration.

You can set up a GitHub Actions workflow to deploy your software product. To verify that your product works as expected, your workflow can build the code in your repository and run your tests before deploying.

You can configure your CD workflow to run when a GitHub event occurs (for example, when new code is pushed to the default branch of your repository), on a set schedule, manually, or when an external event occurs using the repository dispatch webhook.

GitHub Actions provides features that give you more control over deployments. For example, you can use environments to require approval for a job to proceed, restrict which branches can trigger a workflow, or limit access to secrets. You can use concurrency to limit your CD pipeline to a maximum of one in-progress deployment and one pending deployment.

## Using OpenID Connect to access cloud resources

---

If your GitHub Actions workflows need to access resources from a cloud provider that supports OpenID Connect (OIDC), you can configure your workflows to authenticate directly to the cloud provider. This will let you stop storing these credentials as long-lived secrets and provide other security benefits.

## Starter workflows and third party actions

---

GitHub offers deployment starter workflows for several popular services, such as Azure Web App.

### More information

- [Deploying nodeJS to azure app service](https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-nodejs-to-azure-app-service)

Many service providers also offer actions on GitHub Marketplace for deploying to their service.

## Deploying with GitHub Actions

---

In this article

Learn how to control deployments with features like environments and concurrency.

## Introduction

---

GitHub Actions offers features that let you control deployments. You can:

- Trigger workflows with a variety of events.
- Configure environments to set rules before a job can proceed and to limit access to secrets.
- Use concurrency to control the number of deployments running at a time.

You should be familiar with the syntax for GitHub Actions.

## Triggering your deployment

---

You can use a variety of events to trigger your deployment workflow. Some of the most common are: pull_request, push, and workflow_dispatch.

For example, a workflow with the following triggers runs whenever:

- There is a push to the main branch.
- A pull request targeting the main branch is opened, synchronized, or reopened.
- Someone manually triggers it.

```
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:
```

## Using environments

---

Environments are used to describe a general deployment target like production, staging, or development. When a GitHub Actions workflow deploys to an environment, the environment is displayed on the main page of the repository. You can use environments to require approval for a job to proceed, restrict which branches can trigger a workflow, gate deployments with custom deployment protection rules, or limit access to secrets.

## Using concurrency

---

Concurrency ensures that only a single job or workflow using the same concurrency group will run at a time. You can use concurrency so that an environment has a maximum of one deployment in progress and one deployment pending at a time.

For example, when the following workflow runs, it will be paused with the status pending if any job or workflow that uses the production concurrency group is in progress. It will also cancel any job or workflow that uses the production concurrency group and has the status pending. This means that there will be a maximum of one running and one pending job or workflow in that uses the production concurrency group.

```
name: Deployment

concurrency: production

on:
  push:
    branches:
      - main

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: deploy
        # ...deployment-specific steps
```

You can also specify concurrency at the job level. This will allow other jobs in the workflow to proceed even if the concurrent job is pending.

```
name: Deployment

on:
  push:
    branches:
      - main

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment: production
    concurrency: production
    steps:
      - name: deploy
        # ...deployment-specific steps

```

You can also use cancel-in-progress to cancel any currently running job or workflow in the same concurrency group.

```
name: Deployment

concurrency:
  group: production
  cancel-in-progress: true

on:
  push:
    branches:
      - main

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: deploy
        # ...deployment-specific steps

```

## Viewing deployment history

---

When a GitHub Actions workflow deploys to an environment, the environment is displayed on the main page of the repository.

## Monitoring workflow runs

---

Every workflow run generates a real-time graph that illustrates the run progress. You can use this graph to monitor and debug deployments.

## Tracking deployments through apps

---

If your personal account or organization on GitHub.com is integrated with Microsoft Teams or Slack, you can track deployments that use environments through Microsoft Teams or Slack. For example, you can receive notifications through the app when a deployment is pending approval, when a deployment is approved, or when the deployment status changes.

You can also build an app that uses deployment and deployment status webhooks to track deployments. When a workflow job that references an environment runs, it creates a deployment object with the environment property set to the name of your environment. As the workflow progresses, it also creates deployment status objects with the environment property set to the name of your environment, the environment_url property set to the URL for environment (if specified in the workflow), and the state property set to the status of the job.

## Choosing a runner

---

You can run your deployment workflow on GitHub-hosted runners or on self-hosted runners. Traffic from GitHub-hosted runners can come from a wide range of network addresses. If you are deploying to an internal environment and your company restricts external traffic into private networks, GitHub Actions workflows running on GitHub-hosted runners may not be able to communicate with your internal services or resources. To overcome this, you can host your own runners.

## Displaying a status badge

---

You can use a status badge to display the status of your deployment workflow. A status badge shows whether a workflow is currently failing or passing. A common place to add a status badge is in the README.md file of your repository, but you can add it to any web page you'd like. By default, badges display the status of your default branch. You can also display the status of a workflow run for a specific branch or event using the branch and event query parameters in the URL.

## Finding deployment examples

---

This article demonstrated features of GitHub Actions that you can add to your deployment workflows.

GitHub offers deployment starter workflows for several popular services, such as Azure Web App.

Many service providers also offer actions on GitHub Marketplace for deploying to their service.

### More information

- [Deploying to Azure statci web app](https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-to-azure-static-web-app)
- [Deploying Docker to Azure App Service](https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-docker-to-azure-app-service)
- [Deploying Node.JS to Azure App Service](https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-nodejs-to-azure-app-service)

## Security Harden deployments

---

### More information

- [Security Harden deployments](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect)

"Security hardening deployments" refers to the process of implementing measures to enhance the security of software deployments and make them more resistant to security threats and vulnerabilities. It involves adopting various security practices, configurations, and technologies to reduce the risk of unauthorized access, data breaches, and other security incidents.

Here are some key aspects of security hardening deployments:

System Configuration: It involves securely configuring the underlying infrastructure, operating systems, and applications to minimize potential attack vectors. This may include disabling unnecessary services, configuring secure network settings, and applying recommended security settings.

Access Control: Implementing robust access controls ensures that only authorized individuals or systems have appropriate privileges to access and modify the deployed software. This can involve using strong authentication mechanisms, enforcing least privilege principles, and implementing multi-factor authentication where applicable.

Vulnerability Management: Regularly scanning and patching software and systems for known vulnerabilities is crucial for security hardening. This involves keeping the deployed software up to date with security patches, monitoring for vulnerabilities, and promptly applying fixes to minimize the risk of exploitation.

Secure Communication: Ensuring secure communication between components is vital to protect data and prevent interception or tampering. It involves utilizing encryption protocols (such as HTTPS or SSL/TLS) for data transmission, securely configuring communication channels, and implementing secure API integrations.

Logging and Monitoring: Comprehensive logging and monitoring mechanisms help detect and respond to security incidents. This includes logging relevant security events, analyzing logs for suspicious activities, and setting up monitoring systems to alert administrators in case of potential breaches or anomalies.

Incident Response: Having a well-defined incident response plan helps in efficiently handling security incidents if they occur. It involves defining processes, roles, and responsibilities for responding to security events, conducting forensic investigations, and taking necessary actions to mitigate the impact and prevent future incidents.

By applying security hardening practices to deployments, organizations can significantly reduce the risk of security breaches, protect sensitive data, maintain the integrity of deployed software, and ensure the overall security posture of their systems.

## OpenID Configuration for Giuthub Actions

---

### More informatio

- [OpenID Connect for Giuthub Actions](https://token.actions.githubusercontent.com/.well-known/openid-configuration)
- [OpenID Connect in cloud providers](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-cloud-providers)

## Using environments for deployment

---

You can configure environments with protection rules and secrets. A workflow job that references an environment must follow any protection rules for the environment before running or accessing the environment's secrets.

Environments are used to describe a general deployment target like production, staging, or development. When a GitHub Actions workflow deploys to an environment, the environment is displayed on the main page of the repository.

You can configure environments with protection rules and secrets. When a workflow job references an environment, the job won't start until all of the environment's protection rules pass. A job also cannot access secrets that are defined in an environment until all the environment protection rules pass.

Optionally, you can bypass an environment's protection rules and force all pending jobs referencing the environment to proceed.

## Deployment protection rules

---

Deployment protection rules require specific conditions to pass before a job referencing the environment can proceed. You can use deployment protection rules to require a manual approval, delay a job, or restrict the environment to certain branches. You can also create and implement custom protection rules powered by GitHub Apps to use third-party systems to control deployments referencing environments configured on GitHub.com.

Third-party systems can be observability systems, change management systems, code quality systems, or other manual configurations that you use to assess readiness before deployments are safely rolled out to environments.

Any number of GitHub Apps-based deployment protection rules can be installed on a repository. However, a maximum of 6 deployment protection rules can be enabled on any environment at the same time.

## Required reviewers

---

Use required reviewers to require a specific person or team to approve workflow jobs that reference the environment. You can list up to six users or teams as reviewers. The reviewers must have at least read access to the repository. Only one of the required reviewers needs to approve the job for it to proceed.

## Wait timer

---

Use a wait timer to delay a job for a specific amount of time after the job is initially triggered. The time (in minutes) must be an integer between 0 and 43,200 (30 days).

## Deployment branches

---

Use deployment branches to restrict which branches can deploy to the environment. Below are the options for deployment branches for an environment:

All branches: All branches in the repository can deploy to the environment.

Protected branches: Only branches with branch protection rules enabled can deploy to the environment. If no branch protection rules are defined for any branch in the repository, then all branches can deploy.

Selected branches: Only branches that match your specified name patterns can deploy to the environment.

For example, if you specify releases/_ as a deployment branch rule, only branches whose name begins with releases/ can deploy to the environment. (Wildcard characters will not match /. To match branches that begin with release/ and contain an additional single slash, use release/_/\*.) If you add main as a deployment branch rule, a branch named main can also deploy to the environment.

## Allow administrators to bypass configured protection rules

---

By default, administrators can bypass the protection rules and force deployments to specific environments.

Alternatively, you can configure environments to disallow bypassing the protection rules for all deployments to the environment.

## Custom deployment protection rules

---

You can enable your own custom protection rules to gate deployments with third-party services. For example, you can use services such as Datadog, Honeycomb, and ServiceNow to provide automated approvals for deployments to GitHub.com.

Once custom deployment protection rules have been created and installed on a repository, you can enable the custom deployment protection rule for any environment in the repository.

## Environment secrets

---

Secrets stored in an environment are only available to workflow jobs that reference the environment. If the environment requires approval, a job cannot access environment secrets until one of the required reviewers approves it.

## Environment variables

---

Variables stored in an environment are only available to workflow jobs that reference the environment.

## Creating an environment

---

To configure an environment in a personal account repository, you must be the repository owner. To configure an environment in an organization repository, you must have admin access.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.
3. In the left sidebar, click Environments.
4. Click New environment.
5. Enter a name for the environment, then click Configure environment. Environment names are not case sensitive. An environment name may not exceed 255 characters and must be unique within the repository.
6. Optionally, specify people or teams that must approve workflow jobs that use this environment.
   1. Select Required reviewers.
   2. Enter up to 6 people or teams. Only one of the required reviewers needs to approve the job for it to proceed.
   3. Click Save protection rules.
7. Optionally, specify the amount of time to wait before allowing workflow jobs that use this environment to proceed.
   1. Select Wait timer.
   2. Enter the number of minutes to wait.
   3. Click Save protection rules.
8. Optionally, disallow bypassing configured protection rules.
9. Optionally, enable any custom deployment protection rules that have been created with GitHub Apps.
10. Optionally, specify what branches can deploy to this environment. Fo
    1. Select the desired option in the Deployment branches dropdown.
    2. If you chose Selected branches, enter the branch name patterns that you want to allow.
11. Optionally, add environment secrets. These secrets are only available to workflow jobs that use the environment. Additionally, workflow jobs that use this environment can only access these secrets after any configured rules (for example, required reviewers) pass.
    1. Under Environment secrets, click Add Secret.
    2. Enter the secret name.
    3. Enter the secret value.
    4. Click Add secret.
12. Optionally, add environment variables. These variables are only available to workflow jobs that use the environment, and are only accessible using the vars context.
    1. Under Environment variables, click Add Variable.
    2. Enter the variable name.
    3. Enter the variable value.
    4. Click Add variable.

You can also create and configure environments through the REST API.

Running a workflow that references an environment that does not exist will create an environment with the referenced name. The newly created environment will not have any protection rules or secrets configured. Anyone that can edit workflows in the repository can create environments via a workflow file, but only repository admins can configure the environment.

## Using an environment

---

Each job in a workflow can reference a single environment. Any protection rules configured for the environment must pass before a job referencing the environment is sent to a runner. The job can access the environment's secrets only after the job is sent to a runner.

When a workflow references an environment, the environment will appear in the repository's deployments.

You can specify an environment for each job in your workflow. To do so, add a jobs.<job_id>.environment key followed by the name of the environment.

For example, this workflow will use an environment called production.

```
name: Deployment

on:
  push:
    branches:
      - main

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: deploy
        # ...deployment-specific steps
```

When the above workflow runs, the deployment job will be subject to any rules configured for the production environment. For example, if the environment requires reviewers, the job will pause until one of the reviewers approves the job.

You can also specify a URL for the environment. The specified URL will appear on the deployments page for the repository (accessed by clicking Environments on the home page of your repository) and in the visualization graph for the workflow run. If a pull request triggered the workflow, the URL is also displayed as a View deployment button in the pull request timeline.

```
name: Deployment

on:
  push:
    branches:
      - main

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment:
      name: production
      url: https://github.com
    steps:
      - name: deploy
        # ...deployment-specific steps
```

## Deleting an environment

---

To configure an environment in a personal account repository, you must be the repository owner. To configure an environment in an organization repository, you must have admin access.

Deleting an environment will delete all secrets and protection rules associated with the environment. Any jobs currently waiting because of protection rules from the deleted environment will automatically fail.

### Process' checklist

1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.
3. In the left sidebar, click Environments.
4. Next to the environment that you want to delete, click (trash icon).
5. Click I understand, delete this environment.

You can also delete environments through the REST API.

## How environments relate to deployments

---

When a workflow job that references an environment runs, it creates a deployment object with the environment property set to the name of your environment. As the workflow progresses, it also creates deployment status objects with the environment property set to the name of your environment, the environment_url property set to the URL for environment (if specified in the workflow), and the state property set to the status of the job.

You can access these objects through the REST API or GraphQL API.

## Creating custom deployment protection rules

---

### More information

- [Creating custom deployment protection rules](https://docs.github.com/en/actions/deployment/protecting-deployments/creating-custom-deployment-protection-rules)

## Configuring custom deployment protection rules

---

### More information

- [Configuring custom deployment protection rules](https://docs.github.com/en/actions/deployment/protecting-deployments/configuring-custom-deployment-protection-rules)

## Viewing deployment history

---

View current and previous deployments for your repository.

You can deliver deployments through GitHub Actions and environments or with the REST API and third party apps.

To view current and past deployments, click Environments in the sidebar of the home page of your repository.

The deployments page displays the last active deployment of each environment for your repository. If the deployment includes an environment URL, a View deployment button that links to the URL is shown next to the deployment.

The activity log shows the deployment history for your environments. By default, only the most recent deployment for an environment has an Active status; all previously active deployments have an Inactive status.

You can also use the REST API to get information about deployments.

## Deploying Xcode applications

---

### More information

- [Deploying Xcode applications](https://docs.github.com/en/actions/deployment/deploying-xcode-applications/installing-an-apple-certificate-on-macos-runners-for-xcode-development)
