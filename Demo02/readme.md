# Run ASP.NET Core Web App with Docker

At this demo we will run an ASP.NET Core Web App with Docker and Docker Compose.

The Original Sample App is located at [dotnet-architecture/eShopOnWeb](https://github.com/dotnet-architecture/eShopOnWeb), I forked it at my repo and **I made some changes for this workshop** so you can download, clone or fork it: [josema88/eShopOnWeb](https://github.com/josema88/eShopOnWeb).


### Build and Run Docker Container for App
From root directory execute:

```sh
# Build Docker Image
$ docker build --pull -t web -f src/Web/Dockerfile .
```

NOTE: Before run the following steps you should create the Databases and run the Entity Core Migrations as the project's README file specifies. Also you should know the connection strings to set it correctly to the command, I set those values within environment variables in my machine: **CAT_CONNSTR** and **IDE_CONNSTR**.
```sh
# Run App locally with Docker container
$ docker run --name eshopweb --rm -it -d \
-e ASPNETCORE_ENVIRONMENT=Production \
-e "ConnectionStrings:CatalogConnection"="${CAT_CONNSTR}" \
-e "ConnectionStrings:IdentityConnection"="${IDE_CONNSTR}" \
-p 5108:80 web
```
The app should be available at http://localhost:5108/

### Build and Run Docker Container for App with Docker Compose
```sh
# Build image with Docker Compose
$ docker-compose build
```
```sh
# Run App with Docker Compose
$ docker-compose up
```
The app should be available at:
http://localhost:5106/

### Upload Image to Docker Hub with Docker Compose

The image will be built by default with the *latest* tag, therefore the image will be uploaded to the Docker Hub with the same tag.
```sh
$ docker-compose push 
```