# TEOC Infrastructure

This repository contains the Terraform configurations to deploy the `TEOC` service, consisting of two applications: [hello-world-frontend](https://github.com/ntsedemoorg/hello-world-front) and [hello-world-api](https://github.com/ntsedemoorg/hello-world-api). This Terraform repo sets up the necessary Azure infrastructure to run the applications.

## Project Structure

- `applications/`
  - `hello-world-frontend/`: Terraform configuration for deploying the frontend application.
  - `hello-world-api/`: Terraform configuration for deploying the backend API.
- `core-services/`
  - `app-insights/`: Terraform configuration for setting up the app-insight.
  - `app-service-plan/`: Terraform configuration for setting up the app-service-plan.
  - `app-service/`: Terraform configuration for setting up the app-service.
  - `keyvault/`: Terraform configuration for setting up the keyvault.
  - `log-analytics/`: Terraform configuration for setting up the log-analytics.
  - `resource-group/`: Terraform configuration for setting up the resource-group.
- `environment/`
  - `dev.tfvars`: Terraform variables for the development environment.
- `global.tfvars`: Global Terraform variables.
- `providers.tf`: Terraform provider configurations. This file is copied during the Github Actions workflow to each directory where it is needed. CLI flags are then passed in to use the correct backend.
- `terraform.tf`: Terraform version configuration. This file is copied during the Github Actions workflow to each directory where it is needed. 

## Terraform Stacks

Each directory in the `core-services` and `applications` folders has its own Terraform state file. Each directory is called a 'stack'. This isolation allows for modular and independent management of each component of the infrastructure, facilitating easier updates and rollbacks.

With an Azure backend, the state file for each stack is stored in at the key `<environment name>/<directory name>/state.tfstate` in the state bucket. For example, the state file for the `hello-world-api` stack in the `development` environment would be `development/hello-world-api/state.tfstate`.

## Order of Terraform Apply / `dependencies.json`

In each Terraform stack, there is a `dependencies.json`. This **MUST** exist in each stack that you want to deploy. The content of this looks similar to the below and represents the direct dependencies of each stack. The [terraform-dependency-sort](https://github.com/UKHSA-Internal/devops-github-actions/tree/main/.github/actions/terraform-dependency-sort) action finds indirect dependencies of each stack and return a list of stacks, topgraphically sorted into the order it must be applied. This is then used by Github Actions to run the Terraform commands in the correct order of dependency.

The dependencies.json **MUST** validate against the schema below. If there are no dependencies, `paths` can be a blank array.

### Schema

```json
    "$schema": "http://json-schema.org/draft-07/schema#",
    "title": "Dependencies Schema",
    "type": "object",
    "properties": {
        "dependencies": {
            "type": "object",
            "properties": {
                "paths": {
                    "type": "array",
                    "items": {
                        "type": "string",
                    },
                }
            },
            "required": ["paths"],
        }
    },
    "required": ["dependencies"],
```

### Example of a stack with dependencies

```json
{
    "dependencies": {
        "paths": [
            "./core-services/ecs",
            "./core-services/memcached"
        ]
    }
}
```

### Example of a stack with zero dependencies

```json
{
    "dependencies": {
        "paths": []
    }
}
```

## `providers.tf` and `terraform.tf`

Both of these files exist at the root of the project and are copied into each stack as part of the Github Actions workflow. This allows the versions files to be kept [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). This behaviour can be overriden by placing a `provider.tf` or `terraform.tf` file into the stack's directory. However, this **SHOULD NOT** be done as a matter of routine and but can used for extraordinary circumstances.

For more information on the specific modules used and their configurations, refer to the individual Terraform configuration files in each directory.
