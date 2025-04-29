# 1. Containerization

## Goal

In this exercise, you will containerize both the web application and its reverse proxy. The application should be accessible through the reverse proxy over HTTP (port 80).

By the end of this exercise, you will have learned how to use Docker to isolate processes, set up a communication between containers and enable interaction with the host system.

## Task Overview

- Containerize the Flask application: Create a Dockerfile to containerize the Flask web application.
- Containerize HAProxy: Create a Dockerfile for HAProxy to reverse proxy requests to the Flask application.
- Connect the containers in a Docker network: make sure both containers can communicate with each other, but expose only port 80 to the host system (HAProxy should be the only exposed service).

After building and running the containers, you should be able to access the application in your browser via <http://localhost>.

## 1. Containerize the Flask application

Go to the Flask application directory and create a Dockerfile

```bash
cd app
touch Dockerfile
```

Here are the steps you'll have to complete. For each one, try to find and use the correct Dockerfile instruction by referring to the official documentation: <https://docs.docker.com/reference/dockerfile/>.

- Use `python:3.12-slim` as the base image
- Set up the working directory, for example `/usr/local/webapp`.
- Install the required Python packages.
  <details>
  <summary>Hint 1</summary>

  The command to run can be found in the `README.md` of the [devops-101 project](https://gitlab.com/raynnham/devops-101-template). What Dockerfile instruction can be used to execute this command ? 

  </details>
  <details>
  <summary>Hint 2</summary>

  You need to have the `requirements.txt` file present in the container to install the packages. To achieve this, you can either:
  - Copy the file into the container.
  - (Recommended) Use the following option in the Dockerfile instruction: `--mount=type=bind,source=requirements.txt,target=requirements.txt."`

  </details>
- Copy the application files present in `src/` into the container.
- Expose the `3000` port.
- Set the required environment variables for Flask and the application.
  <details>
  <summary>Hint</summary>

  The required environment variables to set can be found in the `README.md` of the [devops-101 project](https://gitlab.com/raynnham/devops-101-template).

  </details>
- Set `flask run` as the command to be executed when running the container.

**Solution**: Will be provided

## 2. Containerize HAProxy

Go to the HAProxy directory and create a Dockerfile.

```bash
cd ../reverse-proxy
touch Dockerfile
```
You can now visit the [official HAProxy image page on Docker Hub](https://hub.docker.com/_/haproxy/) and follow the instructions on how to write the Dockerfile. **The HAProxy configuration file is located in the current folder under the name `haproxy.cfg`**.

**Solution**: Will be provided

## 3. Run the containers

Now that you have created the Dockerfiles for both the Flask application and HAProxy, it's time to run the containers.

Go back to the root of the repository.

```bash
cd ..
```

Here are the steps you'll have to complete. For each one, try to find and use the correct Docker CLI command by referring to the official documentation: <https://docs.docker.com/reference/cli/docker/>.

- Build the Docker images for both the Flask application and HAProxy  
  - Use the appropriate option to assign a custom name to each image  
- Create a Docker network using the `bridge` driver to enable communication between the containers  
- Run both containers  
  - Launch them in detached mode (in the background)  
  - Attach them to the previously created Docker network  
  - Assign each container a meaningful name  
  <details><summary>Hint</summary>  

  You need to bind port 80 of the HAProxy container to port 80 of the host's loopback interface (`127.0.0.1`) so that the application can be accessed locally via the browser.  

  </details>  
- List the currently running Docker containers and verify that you can access the application at <http://localhost>.  
  If needed, use the `docker logs` command to troubleshoot any issues.  

**Solution**: Will be provided

> [!IMPORTANT]
> Once you’ve completed your tests, make sure to clean up your environment before moving on to the next exercise.
> You can use the commands provided in the solution.

## 🎉 Congratulations

**You've completed the first exercise ! You can now move on to the next one [here](/2-Infrastructure-as-Code/README.md).**
