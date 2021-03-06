# docker-examples
- https://github.com/wsargent/docker-cheat-sheet
- https://docs.docker.com/get-started/part2/
- http://containertutorials.com/docker-compose/flask-simple-app.html
- https://jpetazzo.github.io/2013/12/01/docker-python-pip-requirements/

## Cheatsheet
These commands can be copied and pasted and includes a sudo and non-sudo version.

```bash
# Starts a container.
sudo docker start
docker start

# Stop all containers.
sudo docker stop $(sudo docker ps -aq)
docker stop $(docker ps -aq)

# Remove all containers.
sudo docker rm $(sudo docker ps -aq)
docker rm $(docker ps -aq)

# Remove image.
sudo docker rmi <image-id>
docker rmi <image-id>

# Remove all images.
sudo docker rmi $(sudo docker images -q)
docker rmi $(docker images -q)
```

### Building and running a local container

```bash
# Find your new docker image.
sudo docker images
docker images

# Run container (forward ports -> host:guest)
sudo docker run -dit -p 8080:80 <image-id-or-name>
docker run -dit -p 8080:80 <image-id-or-name>

# (Optional) You can also specify the container name.
sudo docker run -dit -p 8080:80 <image-id-or-name> -name <container-name>
docker run -dit -p 8080:80 <image-id-or-name> -name <container-name>

# Debug exited containers by removing the '-d' flag.
sudo docker run -it <image-id-or-name>
docker run -it <image-id-or-name>

# Run container with synced volume from host to guest.
sudo docker run -dit -p 8080:80 -v $(pwd):<guest-dir> <image-name>
docker run -dit -p 8080:80 -v $(pwd):<guest-dir> <image-name>

# Example: /darth_varder/ will be available in guest.
sudo docker run -it -v $HOME/Workspace/tf_files:/darth_vader c3efccc5f94f
docker run -it -v $HOME/Workspace/tf_files:/darth_vader c3efccc5f94f

# Lists all available containers and list just the container ids.
sudo docker ps -aq
docker ps -aq

# SSH into container via attachment (halts process if you exit).
sudo docker attach <container-id>
docker attach <container-id>

# SSH into container via new process (won't halt if you exit).
sudo docker exec -it <container-id> bash
docker exec -it <container-id> bash
```

### Basic Setup
```bash
sudo docker build -t nltk-flask .
sudo docker run -dit -p 5000:5000 nltk-flask
```

Then visit: http://localhost:5000

```bash
# To enter container, run:
sudo docker ps
sudo docker exec -it <container-id-or-name> bash

# While inside container use exit to prevent shutting down container.
$ exit
```

## Publishing container to Dockerhub

```bash
# Build image locally.
sudo docker build -t <username>/<repo> .

# Create a Dockerhub account.
https://hub.docker.com/

# Log into your Dockerhub account in your terminal.
sudo docker login

# Publish container
sudo docker push <username>/<repo>
```

## Docker on MacOS

https://docs.docker.com/docker-for-mac/

This link will tell you everything about setting up docker for Mac, what the GUI does,
how to setup preferences, how to start file sharing, and how to perform more advanced
tasks such as setting up certificates.

### Setup
Try to run this simple command to spin up a new nginx docker webserver.
```bash
sudo docker run -d -p 80:80 --name webserver nginx
```

If you see this error, then open up Docker application via GUI with CMD+space, then
type docker. It will tell you to install and relaunch docker.
```bash
docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
```

Once that's complete you can stop or remove the web server container.
```bash
sudo docker stop webserver
sudo docker rm -f webserver
sudo docker rmi nginx
```
