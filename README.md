# DevOps 101 

Welcome to this DevOps training ! The goal of this project is to introduce DevOps concepts and provide you with an overview of related tools and methods.

You will start with a simple web application and progressively enrish it by exploring and applying key DevOps principles, such as Containerization, Infrastructure as Code, CI/CD, and Monitoring.

## Prerequisites

- A [Gitlab account](https://gitlab.com/) linked to an ssh key you own
  - [Create an ssh key](https://docs.gitlab.com/ee/user/ssh.html#generate-an-ssh-key-pair)
  - [Add the key to your Gitlab account](https://docs.gitlab.com/ee/user/ssh.html#add-an-ssh-key-to-your-gitlab-account)
- [Git](https://www.atlassian.com/git/tutorials/install-git )
- [Docker](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository )
- [Terraform](https://developer.hashicorp.com/terraform/install#linux)
- [Gitlab Runner](https://docs.gitlab.com/runner/install/linux-repository/#install-gitlab-runner)

## Getting started

- Create a new blank Gitlab project named `devops-101`
> [!IMPORTANT]
> Uncheck the README creation
- Clone your created repository
- Clone the `devops-101-template` repository : `git clone git@gitlab.com:raynnham/devops-101-template.git`
- Copy all the content of the `devops-101-template` repository into your newly created repository
  - Do not copy the `.git` directory ! It should already be there when you create the repository
- Your directory should look like :
  
  ```bash
  ├── app/
  ├── .git/
  ├── .gitignore
  ├── README.md
  └── reverse-proxy/
  ```
--> Take a look at the project README.md

- Run these commands at the root of your new repository :
  
```bash
git switch -c main
git add .
git commit -m "Initial commit"
git push -u origin main
```

**You can now follow the exercices in order, starting [here](/1-Containerization/README.md) !**
