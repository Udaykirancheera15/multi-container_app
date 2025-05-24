This project is a simple TODO application created to test and enhance my knowledge of containerization using Docker. It demonstrates a multi-container setup utilizing Docker Compose to manage the application’s architecture.
Features

    Multi-container architecture (frontend, backend, and database)
    Easy deployment using Docker Compose
    Interactive TODO list functionality

Prerequisites

    Docker Desktop installed
    Docker Compose

Setup Instructions

    Clone the repository:

    bash

git clone https://github.com/Udaykirancheera15/multi-container-app.git

Build the Docker images:

bash

docker-compose build

Start the application:

bash

    docker-compose up

    This will start both the TODO app and the MongoDB database containers.

    Access the application:

    Open your web browser and go to http://localhost:3000.

    MongoDB Database:

    The MongoDB service will be running on localhost:27017 (default MongoDB port), but it is only accessible by the application and not exposed externally.

Project Structure

    app/: Contains the frontend and backend code for the TODO app.
    Dockerfile: Defines how to build the TODO app container.
    docker-compose.yml: Defines the services (TODO app and MongoDB) and how they interact.

Example docker-compose.yml:

yaml

services:
  todo-app:
    build:
      context: ./app
    depends_on:
      - todo-database
    environment:
      NODE_ENV: production
    ports:
      - 3000:3000
      - 35729:35729
    develop:
      watch:
        - path: ./app/package.json
          action: rebuild
        - path: ./app
          target: /usr/src/app
          action: sync

  todo-database:
    image: mongo:6
    ports:
      - 27017:27017

Breakdown:

    todo-app: This service builds the Node.js and React TODO application and exposes it on port 3000.
    todo-database: This service uses the official MongoDB image (mongo:6) and exposes MongoDB on port 27017.

Running in Development Mode

The configuration supports live reloading and code syncing for the TODO app when running in development. The develop section in the docker-compose.yml watches the package.json and the app codebase for changes, triggering a rebuild or syncing changes automatically.
Stopping the Application

To stop the application, run:

bash

docker-compose down

This will stop and remove the containers, but the data stored in the MongoDB container will be lost unless volumes are defined.
License
It is based on a Docker tutorial and includes modifications demonstrating my understanding of Docker and containerization principles.
