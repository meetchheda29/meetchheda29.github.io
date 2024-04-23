## Building a Three-Layer Website with Docker: A Step-by-Step Guide

### Introduction:
In modern web development, containerization has become a popular approach for deploying applications due to its ease of use and scalability. Docker, a leading containerization platform, allows developers to encapsulate applications and their dependencies into containers. In this guide, we'll walk through the process of building a three-layer website using Docker containers, consisting of a frontend, a backend, and a database.

Docker has revolutionized software development by popularizing containerization. Here's a brief overview of what Docker and containers are all about.Containers are lightweight, standalone packages that include all the necessary components to run an application. They share the host operating system kernel, making them highly efficient and portable.

Images: Immutable templates containing application code, dependencies, and settings.

Containers: Runnable instances of Docker images, isolated from one another.

Dockerfile: Text file specifying instructions for building Docker images.

Docker Engine: Core component managing Docker containers and images.

Today, we embark on an exhilarating journey through the realm of containerization, where we’ll Dockerize a magnificent three-tier application. Are you ready to dive into the world of Docker and witness the magic of containerization? Let’s get started!

### Step 1: Setting Up Directories:
Create a new folder name website_conatiner and in it add two new folder named as frontend and backend. Also create a YAML file named compose.yaml.
```tsql
website_container/
│
├── frontend
├── backend
└── compose.yaml
```
Once you have the same file structure, you can move to the next part.

### Step 2: Setting Up the Frontend:
Now we'll explore how to set up a frontend application using React and Docker.You must add your own react application in this directory. To create the conatiner of the react app, you need to create a Dockerfile in the frontend folder.

```tsql
frontendd/
│
├── your front end code
└── Dockerfile
```

In this Dockerfile u need to add the following code:- 

```tsql
# Use official Node.js image as the base image
FROM node:alpine as build
# Set working directory
WORKDIR /app
# Copy package.json and package-lock.json files
COPY package*.json ./
# Install dependencies
RUN npm install
# Copy the entire project
COPY . .
# Build the project
RUN npm run build
# Use Nginx as the production server
FROM nginx:alpine
# Copy build files from the previous stage to Nginx directory
COPY --from=build /app/build /usr/share/nginx/html
# Expose port 80 to the outside world
EXPOSE 80
```

#### Some T-SQL Code



#### Some PowerShell Code

```powershell
Write-Host "This is a powershell Code block";

# There are many other languages you can use, but the style has to be loaded first

ForEach ($thing in $things) {
    Write-Output "It highlights it using the GitHub style"
}
```

