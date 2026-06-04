## PROJECT TITLE.

~Dockerized Nginx Static Website~

## Project Description.

This project is a simple Dockerized static website using Nginx.
The goal is to understand Docker concepts like Dockerfile, Docker image, and container.

## Tools used.

nginx
html
dockerfile
dockerimage
container

## File structure.

dockerized-website/
    -index.html
    -dockerfile
    -README.md

## Dockerfile instructions used.

FROM
COPY

## To build a Docker image.

$ docker build -t 'image name' 'file path'

-t = used to give a new name to a image.

## To build a container using Docker image.

$ docker run -d -p 80:80 --name 'container name' 'image name' 

             -d = to run the container in detachmod (background).

                -p = stands for publish. To bind host port into container port.

                   80:80 = HostPort:ContainerPort , need to do it manually.

                         --name = to give a name to the container.

## To access the container from outside.

http://localhost:80

or EC2

http://EC2public-ip

In EC2 add port 80 in sg inbound rule and source need to be 0.0.0.0/0 (ip from anywhere).

## Troubleshooting.

Security group blocking access (EC2)

## What and why i didnt use RUN , CMD & WORKDIR.

RUN = I did not use RUN because the base image nginx already contains all required dependencies and Nginx is pre-installed.

CMD = I did not use CMD because the official Nginx image already defines a default CMD that starts the Nginx server automatically when the container runs.

WORKDIR = I did not use WORKDIR because I directly copied the index.html file into Nginx’s default web directory.

## Architecture

User -> Docker Container -> Nginx -> HTML Page


