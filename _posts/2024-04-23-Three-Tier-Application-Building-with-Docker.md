## Building a Three-Layer Website with Docker: A Step-by-Step Guide

### Introduction :
In modern web development, containerization has become a popular approach for deploying applications due to its ease of use and scalability. Docker, a leading containerization platform, allows developers to encapsulate applications and their dependencies into containers. In this guide, we'll walk through the process of building a three-layer website using Docker containers, consisting of a frontend, a backend, and a database.

Docker has revolutionized software development by popularizing containerization. Here's a brief overview of what Docker and containers are all about.Containers are lightweight, standalone packages that include all the necessary components to run an application. They share the host operating system kernel, making them highly efficient and portable.

-**Images:** Immutable templates containing application code, dependencies, and settings.

-**Containers:** Runnable instances of Docker images, isolated from one another.

-**Dockerfile:** Text file specifying instructions for building Docker images.

-**Docker Engine:** Core component managing Docker containers and images.

Today, we embark on an exhilarating journey through the realm of containerization, where we’ll Dockerize a magnificent three-tier application. Are you ready to dive into the world of Docker and witness the magic of containerization? Let’s get started!

### Step 1: Setting Up Directories and Docker:
Create a new folder name website_conatiner and in it add two new folder named as frontend and backend.
```tsql
website_container/
│
├── frontend
├── backend
```
Once you have the same file structure, you can move to the next part.

Before jumping into coding, you make sure your docker is up to date and your Docker Desktop is running.

### Step 2: Setting Up the Frontend:
Now we'll explore how to set up a frontend application using React and Docker.You must add your own react application in this directory. To create the conatiner of the react app, you need to create a Dockerfile in the frontend folder.

```tsql
frontend/
│
├── your front end code
└── Dockerfile
```

In this Dockerfile you need to add the following code:- 

```powershell
FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]

```

Once your are done with these, you can now create the image for the same by executing the below code in the frontend directory:- 
```powershell
docker build -t my-react-app .
```
A image name my-react-app will be created for the front end.

You can view the image in Docker Desktop or by executing below command:-
```powershell
docker images ls
```

### Step 3: Setting Up the Backend:
Similar to the frontend, we'll create a Dockerfile for our backend Node.js application..You must add your own node application in this directory. To create the conatiner of the node app, you need to create a Dockerfile in the backend folder.

```tsql
backend/
│
├── your back end code(app.js)
└── Dockerfile
```

In this Dockerfile you need to add the following code:- 

```powershell
FROM node:alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

Once your are done with these, you can now create the image for the same by executing the below code in the frontend directory:- 
```powershell
docker build -t my-node-app .
```
A image name my-node-app will be created for the back end.

If you have done till here.Great Work Guys!!!Now we will integrate these images.

### Step 4: Final Integration:

To integrate our Docker images seamlessly, we'll create a docker-compose.yml file in the root directory of our project. This file will define the services required for our blog application and specify how they should interact with each other.
```tsql
website_container/
│
├── frontend
├── backend
└── compose.yaml
```
Now in this compose.yaml file write the below code:- 

```powershell
version: '3'

services:
  frontend:
    image: my-react-app
    ports:
      - "3000:3000"

  backend:
    image: my-node-app
    restart: always
    ports:
      - "3001:3001"
    depends_on:
      - mongodb
    environment:
      - MONGO_URI="Your MongoDB URI"

  mongodb:
    image: mongo
    restart: always
    container_name: mongodb
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_DATABASE=test
      - MONGO_INITDB_ROOT_USERNAME=usernmae
      - MONGO_INITDB_ROOT_PASSWORD=pwd
```

#### Explaining the Compose File:

We define three services: frontend, backend, and mongodb.

The frontend service uses the my-react-app Docker image and maps port 3000 of the host to port 3000 of the container.

The backend service uses the my-node-app Docker image, sets it to restart always, and maps port 3001.

The mongodb service uses the official MongoDB Docker image, sets it to restart always, and maps port 27017.

### Step 5: Running the images together:
To start our integrated application, we simply run the ```powershell docker-compose up ``` command in the terminal. Docker Compose reads the docker-compose.yml file, pulls the necessary images, creates containers, and starts the services defined in the file.

Once you execute the command you will be able to see the running containers in the Docker Desktop.

Here's how you can view the output for each service in your Docker Compose setup:

### Step 6: Accessing the website

Frontend Service (frontend):
You can access frontend by opening a web browser and navigating to http://localhost:3000. This URL corresponds to the port mapping defined in your docker-compose.yml file for the frontend service.

Backend Service (backend):
Your backend is running on http://localhost:3001

MongoDB Service (mongodb):
You generally won't directly view the output of the MongoDB service in a web browser. Instead, you can interact with the MongoDB database using a MongoDB client or command-line tools like mongo.

### CONCLUSION
By Dockerizing both the frontend and backend of our full-stack three-tier application, we've created portable and isolated environments for running our application. Docker simplifies the deployment process, ensures consistency across different environments, and enables scalability. This approach is beneficial for both development and production environments, making it easier to manage and scale our full-stack application effectively.

