# Dockerized Nginx Static Website

A simple static website served using **Nginx inside a Docker container**.

This project was created to understand the fundamentals of Docker, including:

* Dockerfiles
* Docker images
* Docker containers
* Port mapping
* Serving a website using Nginx
* Deploying a Dockerized website on an EC2 instance

## Project Overview

The website is built with a simple `index.html` file and served using the official Nginx Docker image.

The Dockerfile uses:

* `FROM` to define the base image
* `COPY` to copy the website files into the Nginx web directory

## Technologies Used

* HTML
* Nginx
* Docker
* Dockerfile
* Docker Image
* Docker Container
* AWS EC2 *(for optional cloud deployment)*

## Project Structure

```text
dockerized-website/
├── Dockerfile
├── index.html
└── README.md
```

## Dockerfile

The Dockerfile uses the official Nginx image:

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```

### Dockerfile Instructions Used

#### `FROM`

Defines the base image for the Docker image.

In this project, the official Nginx image is used as the base image.

#### `COPY`

Copies the local `index.html` file into the default Nginx web directory inside the container.

```text
/usr/share/nginx/html/
```

## Build the Docker Image

Run the following command from the project directory:

```bash
docker build -t dockerized-website .
```

### Explanation

* `docker build` — Builds a Docker image.
* `-t` — Assigns a name and optional tag to the image.
* `dockerized-website` — The name of the image.
* `.` — Uses the current directory as the build context.

## Run the Docker Container

```bash
docker run -d -p 80:80 --name dockerized-website-container dockerized-website
```

### Explanation

#### `-d`

Runs the container in detached mode, which means it runs in the background.

#### `-p 80:80`

Maps the host port to the container port.

```text
Host Port:Container Port
80:80
```

This allows traffic received on port `80` of the host machine to reach port `80` inside the Docker container.

#### `--name`

Assigns a custom name to the container.

```text
dockerized-website-container
```

## Access the Website

After starting the container, open:

```text
http://localhost
```

You can also use:

```text
http://localhost:80
```

## Deploying on AWS EC2

If the Docker container is running on an EC2 instance, access the website using:

```text
http://<EC2-PUBLIC-IP>
```

### EC2 Security Group Configuration

To access the website from the internet:

1. Open the EC2 instance's Security Group.
2. Add an inbound rule for:

   * **Type:** HTTP
   * **Port:** 80
   * **Source:** `0.0.0.0/0`

> **Security Note:** Allowing `0.0.0.0/0` allows access from anywhere on the internet. For production environments, restrict access where possible.

## Troubleshooting

### Website Cannot Be Accessed on EC2

Check the following:

* The Docker container is running.
* Port `80` is correctly mapped.
* The EC2 Security Group allows inbound HTTP traffic on port `80`.
* The EC2 instance has a public IP address.
* The server's local firewall is not blocking port `80`.

You can check running containers with:

```bash
docker ps
```

## Why Were `RUN`, `CMD`, and `WORKDIR` Not Used?

### `RUN`

`RUN` is not required in this project because the official Nginx base image already contains the Nginx software and its required dependencies.

### `CMD`

`CMD` is not required because the official Nginx image already provides a default command that starts the Nginx server when the container runs.

### `WORKDIR`

`WORKDIR` is not required because the website file is copied directly into Nginx's default web root directory:

```text
/usr/share/nginx/html/
```

## Architecture

```text
        User
          │
          ▼
   Docker Container
          │
          ▼
        Nginx
          │
          ▼
     index.html
          │
          ▼
      Web Page
```

## Learning Outcome

Through this project, I learned the basics of:

* Creating a Dockerfile
* Building a Docker image
* Running a Docker container
* Mapping host and container ports
* Serving a static website using Nginx
* Deploying a Dockerized application on an AWS EC2 instance

This project is a beginner-friendly introduction to containerizing and deploying a static website with Docker.
