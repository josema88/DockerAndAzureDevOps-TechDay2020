# Run Node JS Web App with Docker

At this demo we have a simple Web App that runs in NodeJS that serves static content, we will run it with Docker and Docker Compose.

You can find the Sample at my repo and so you can download or clone it: [josema88/az24esp-webapp](https://github.com/josema88/az24esp-webapp).


### Build and Run Docker Container for App
From root directory execute:

```sh
# Login to Docker Hub
$ docker login

# Configure environment Variable for Docker Hub Id
# You should set your dockerid and a slash at the end
# For me is: josemaord/
# This command is for Mac and Linux
$ export DOCKER_REGISTRY=yourDockerIdAndSlash

# Build Docker Image
$ docker build -t ${DOCKER_REGISTRY}az24esp .
```

```sh
# Run App locally with Docker container
$ docker run -it -d -p 80:8080 ${DOCKER_REGISTRY}az24esp
```
The app should be available at:
http://localhost:80/

### Upload Image to Docker Hub

The image will be built by default with the *latest* tag, therefore the image will be uploaded to the Docker Hub with the same tag.
```sh
$ docker push ${DOCKER_REGISTRY}az24esp