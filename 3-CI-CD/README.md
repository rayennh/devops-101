# 3. CI/CD

## Goal

In this exercise, you will set up a CI/CD pipeline for the application.

By the end of the exercise, you will have learned how to use Gitlab to automate testing and deployment processes.

## Prerequisites

### Python

Make sure python3 and pip are installed.

```bash
python3 --version
pip3 --version
```

If they are not, install them.

```bash
sudo apt update && sudo apt install -y python3 python3-pip
```

### Gitlab runner configuration

Open your project on Gitlab and go to Settings -> CI/CD -> Runner.

First uncheck `Enable instance runners for this project`.
Then click on `New project runner`.

- Check the `Run untagged jobs` box.
- Check the `Lock to current projects` box.

Click on `Create runner`. You will be directed to a page to register the runner. Copy the authentication token that is provided.

Open a new terminal and enter:

```bash
cd /tmp
gitlab-runner register
```

When prompted, provide:

- The Gitlab url: `https://gitlab.com/`
- The token previously copied
- `shell` as the executor.

Make sure the runner is valid and running with:

```bash
gitlab-runner status
gitlab-runner verify
gitlab-runner run
```

Keep this terminal open to let the Gitlab runner process run

## Task Overview

For each step, try to find and use the correct keywords by referring to the official Gitlab CI/CD YAML syntax reference:
<https://docs.gitlab.com/ci/yaml/>.

You will start with a simple pipeline and enrich it.

## 1. Write a simple Gitlab CI/CD configuration

Go to the root of the project and create a Gitlab CI/CD configuration file.

```bash
touch .gitlab-ci.yml
```

Configure a simple pipeline that contains two jobs:

1. `test` job
   - Runs pytest on the application code.
     <details>
     <summary>Hint</summary>
  
     Here is how the `script` part could look like:

     ```yml
     script:
       - python3 -m venv venv          
       - source venv/bin/activate      
       - pip install --upgrade pip     
       - pip install -r app/requirements.txt  
       - pip install pytest            
       - pytest
     ```

     </details>

2. `deploy` job
   - Initializes and applies the Terraform configuration in the `infra/` folder.
     <details>
     <summary>Hint</summary>
  
     Here is how the `script` part could look like:

     ```yml
     script:
       - cd infra
       - terraform init
       - terraform apply -auto-approve
     ```

     </details>

To test and run the pipeline, push your changes to the repository:

```bash
git add .
git commit -m "Add a simple CI/CD pipeline"
git push
```

To follow the execution of the pipeline, go to the repository on Gitlab -> Build -> Pipelines. Once the pipeline is done, check that the Flask application and HAProxy are up and running.

```bash
docker ps
curl http://localhost
```

## 2. Improve the Gitlab CI/CD pipeline

It is now time to improve this simple pipeline by introducing better practices and finer control.

Here are the tasks you need to complete.

### 1. Add a Terraform plan job

Before applying changes, it is a recommended to run terraform plan to preview what will happen.

- Create a new job that runs terraform plan inside the infra/ folder.
  <details>
     <summary>Hint</summary>
  
     Here is how the `script` part of the plan job could look like:

     ```yml
     script:
       - cd infra
       - terraform init
       - terraform plan -out=tf.plan
     ```

   </details>
- Store the generated Terraform plan output as an artifact so it can be used by the apply job. Adapt the apply job so that it uses the plan output file.
  <details>
     <summary>Hint</summary>
  
     Here is how the `script` part of the apply job could look like:

     ```yml
     script:
       - cd infra
       - terraform init
       - terraform apply -auto-approve tf.plan
     ```

   </details>
- Set the apply job to manual

### 2. Deploy only on the main branch

To make sure not to deploy from random branches, add a rule so that the apply job only runs on the main branch.

Check which predefined Gitlab CI/CD variable you can use here: <https://docs.gitlab.com/ci/variables/predefined_variables/#predefined-variables>.

**Solution**: Will be provided

## 🎉 Congratulations

**You've completed the third exercise ! You can now move on to the next one [here](/4-Monitoring/README.md).**
