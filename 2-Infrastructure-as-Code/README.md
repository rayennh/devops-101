# 2. Infrastructure as Code

## Goal

In this exercise, you will manage the applications containers with Infrastructure as Code.

By the end of the exercise, you will have learned how to use Terraform to declare and provision an infrastructure.

> [!NOTE]
> Terraform is used here in a local environment for educational purposes to demonstrate the principles of Infrastructure as Code (IaC).
> While it works in this setup, it is often not the most practical solution for managing containers. Terraform is typically used in conjunction
> with other tools to provision and manage the infrastructure, but not for orchestrating containers directly.

## Task Overview

- Define and create the required infrastructure: a Docker network and two containers (Flask app and HAProxy).
- Apply your configuration and verify that the app is accessible through http://localhost.

## 1. Write the Terraform configuration

Create a new directory to manage the infrastructure and create a Terraform configuration file inside.

```bash
mkdir infra
cd infra
touch main.tf
```

Here are the steps you'll have to complete. For each one, try to find and use the correct Terraform blocks by referring to the official Terraform Docker provider documentation:
<https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs>.

- Use the `terraform` block to specify the required provider and configure the backend to store the state file locally at the `/tmp/terraform.tfstate` path.
  <details>
  <summary>Solution</summary>

  ```tf
  terraform {
    required_providers {
      docker = {
        source  = "kreuzwerker/docker"
        version = "3.0.2"
      }
    }
    backend "local" {
      path = "/tmp/terraform.tfstate"
    }
  }
  ```

  </details>
- Create the provider configuration, but keep it empty
  <details>
  <summary>Solution</summary>

  ```tf
  provider "docker" {}
  ``` 

  </details>
- Create the docker network
- Create the docker image and the docker container for the Flask application
- Create the docker image and the docker container for HAProxy
<details>
<summary>Hint</summary>

Make sure both containers are attached to the network, and only HAProxy is exposed to the host !

</details>

**Solution**: Will be provided

## 2. Apply the Terraform configuration

Now that you have created the Terraform configuration, it's time to apply it.

Here are the steps you'll have to complete. For each one, try to find and use the correct Terraform CLI command by referring to the official documentation: <https://developer.hashicorp.com/terraform/cli/commands>.

- Initialize the working directory
- Creates an execution plan, to preview the changes that Terraform plans to make to the infrastructure. Save the generated plan to a file named `tf.plan`
  <details>
  <summary>Hint</summary>

  What option should be used with the command to save the generated plan to a file ?

  </details>
- Execute the actions proposed in the Terraform plan. Don't forget to specify the plan file !

You should be able to access the app at: <http://localhost>

**Solution**: Will be provided

> [!IMPORTANT]
> Once you’ve completed your tests, make sure to clean up your environment before moving on to the next exercise.
> You can use the command provided in the solution.

## 🎉 Congratulations

**You've completed the second exercise ! You can now move on to the next one [here](/3-CI-CD/README.md).**
