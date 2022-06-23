# Intro to Docker
- Docker is an application that allows you to create containers for applications or software. It puts everything an app needs to run into a simple imgae.

- Docker has a platform similar to GitHub where people can push their apps and others can pull them.

- Docker allows for consistent performace because all dependencies are tested before pushing.

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

```
FROM continuumio/miniconda3:4.10.3p1
RUN conda install \
    xarray \ 
    netCDF4 \ 
    bottleneck \
    numpy \
    pandas \
    matplotlib \
    jupyterlab
CMD ["jupyter-lab","--ip=0.0.0.0","--no-browser","--allow-root"]
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

### `docker build` 
- This is the command that initializes the building of the image from the dockerfile.
- This is also where you can name you own custom image.
- It is important to run this command in the directory with the dockerfile

## Images
- A docker image is what is created from the dockerfile.
- This is the packaged software that can be downloaded and ran quickly.
- Think of it as a template for the app.

#### Pull and Push
- `docker pull` is used to pull exsisting images from dockerhub
- `docker push` if you created an image from a dockerfile, this command is used to push it to dockerhub

## Containers 
- When you pull an image from dockerhub, you can run it to create a container.
- A new container is created and it becomes your own software.
- It is ran side by side to your operating system. Extremely lightweight

#### `docker run`
- This command creates a __new__ container from an exsisting image. 
- This is where some important flags or commands are needed to customize an image.
- It will also automatically start running

#### `docker stop`
- This command stops a container

#### `docker start`
- This commands start an exsisting container

## Best Practices and Commands

#### `docker ps`
- This command will list containers being run currently
- Adding the `-a` will list all containers 

#### `docker rm {NAME}`
- This will remove the container with the name entered

#### `docker exec`
- This is a powerful command that is useful when you need to enter into the container.
- You may need to find the exact command your container needs to run.
