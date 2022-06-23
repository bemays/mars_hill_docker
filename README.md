# Intro to Docker
- Docker is an application that allows you to create containers for applications or software. It puts everything an app needs to run into a simple image.

- Docker has a platform similar to GitHub where people can push their apps and others can pull them.

- Docker allows for consistent performance because all dependencies are tested before pushing.

- Docker images can be deployed in a cloud enviroment such as Azure to host a website.

# How does it work?

![](res/image1.jpg)

## Dockerfile
- It starts with writing a dockerfile. This is a text file, __do not add extension__ only "Dockerfile", that contains the base information the app needs to run.

- In most cases, we do not need to worry about this because the images we will use are already made for us.

```
FROM python:3.10

COPY . /app

RUN pip install -r requirements.txt

CMD ["python3.10","iris.py"]
```

#### FROM
- The FROM clause takes an exsisting image from dockerhub as the base image to build your app off of.

- It is good practice to pick the most basic software your app needs

#### COPY
- This is where we add files we need inside the container. 

- The "." selects everything inside the directory the dockerfile is located, then adds them to /app directory in the container.

#### RUN
- This is a command that is run when docker builds the image. It is usually the command to install other software you need for the app.

#### CMD
- When the container is done being built, this is the commmand that will deploy whatever you want it to do.

### `docker build {OPTIONS}` 
- This is the command that initializes the building of the image from the dockerfile.
- This is also where you can name you own custom image.
- It is important to run this command in the directory with the dockerfile

## Images
- A docker image is what is created from the dockerfile.
- This is the packaged software that can be downloaded and ran quickly.
- Think of it as a template for the app.

#### Pull and Push
- `docker pull {OPTIONS}` is used to pull exsisting images from dockerhub
- `docker push {OPTIONS}` if you created an image from a dockerfile, this command is used to push it to dockerhub

## Containers 
- When you pull an image from dockerhub, you can run it to create a container.
- A new container is created and it becomes your own software.
- It is ran side by side to your operating system. Extremely lightweight

#### `docker run {OPTIONS}`
- This command creates a __new__ container from an exsisting image. 
- It will also automatically start running
- This is where some important flags or commands are needed to customize an image.
  - We may want to attach some files to the container
  - docker run --name {NAME} -v {PATH/TO/VOLUME}:{PATH/IN/CONTAINER} {IMAGE NAME}
  - The path for the container workspace will be different and will require some research

#### `docker stop {OPTIONS}`
- This command stops a container

#### `docker start {OPTIONS}`
- This commands start an exsisting container
- We will want to use the `-i` flag in most cases. This allows us to see what is happening.

## Best Practices and Commands

#### `docker ps {OPTIONS}`
- This command will list containers being run currently
- Adding the `-a` will list all containers 

#### `docker rm {OPTIONS}`
- This will remove the container with the name entered

#### `docker exec {OPTIONS}`
- This is a powerful command that is useful when you need to enter into the container.
- You may need to find the exact command your container needs to run.

## VS Code and Docker
- In order to use docker with VS code you need to download two extensions.
  - "Docker" and "Remote - Containers"

