Back: [Github Actions](./gha.md)

# Github Actions enviroments

## Using environments for jobs

---

Specify an environment for a job.

Use jobs.<job_id>.environment to define the environment that the job references. All environment protection rules must pass before a job referencing the environment is sent to a runner.

You can provide the environment as only the environment name, or as an environment object with the name and url. The URL maps to environment_url in the deployments API.

## Example: Using a single environment name

---

```
environment: staging_environment
```

## Example: Using environment name and URL

---

```
environment:
name: production_environment
url: https://github.com

```

The value of url can be an expression. Allowed expression contexts: github, inputs, vars, needs, strategy, matrix, job, runner, and env.

## Example: Using output as URL

---

```
environment:
name: production_environment
url: ${{ steps.step_id.outputs.url_output }}
The value of name can be an expression. Allowed expression contexts: github, inputs, vars, needs, strategy, and matrix. For more information about expressions, see "Expressions."
```

## Example: Using an expression as environment name

---

```
environment:
name: ${{ github.ref_name }}
```
