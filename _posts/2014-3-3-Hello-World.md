---
layout: post
title: Setting Up the Multi-Container Application with Docker
---
---
Introduction
---
Docker is a widely-used open-source platform designed to streamline the deployment process of applications within lightweight and portable containers. These containers encompass an application along with all its prerequisites, such as libraries, frameworks, and other essential elements, creating a unified package. This encapsulation ensures consistent and dependable performance of the application across various environments, irrespective of the underlying infrastructure.

A notable advantage of Docker is its capability to resolve the common "works on my machine" challenge frequently encountered by software development teams. By bundling applications into containers, developers can ensure consistent behavior across development, testing, and production environments. This uniformity simplifies the development workflow and minimizes the occurrence of deployment-related issues.


Prerequisites
--
Before we begin, ensure you have the following prerequisites:
  Install docker on your machine so for that download docker desktop
  ![image](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/b9fd9e60-3623-42c0-bda0-5485ac816014)
  Basic understanding of Docker concepts
  Knowledge of your application’s frontend and backend technologies through docker documents:

Part 1: Docker Setup
--
Step 1: installing Docker
-
To install Docker, follow these steps:

1. Visit the Docker website and download the appropriate installer for your operating system.
2. Run the installer and follow the on-screen instructions.
3. Once installation is complete, verify that Docker is installed by running docker --version in your terminal.

Step 2: Docker Basics
-
**Image:** Within Docker, an image functions as a self-contained software package capable of executing a specific application or service. It encapsulates the application's code, runtime configurations, essential system libraries, dependencies, and other essential files required for its operation.

**Container:** A Docker container resembles a portable package containing all the essentials for an application to run smoothly. It comprises the application along with necessary tools and configurations. These containers operate independently on your device, with each container's data kept separate from others'.

**Dockerfile:** A text file housing all the instructions necessary to construct a Docker image.

Part 2: Creating Docker Images
--
Step 3: Create Dockerfile for frontend
-
Create a Dockerfile for the frontend application (assuming it’s built with React). Here’s an example:

![image](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/733da117-efb8-4d53-a1f7-69e2805cdd1e)

Step 4: Create Dockerfile for Backend 
-
Create a similar Dockerfile for the backend application.

![image](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/550b0f99-bb2e-44e4-baa9-731c9ef0f307)

Step 5: Building the images
-
You can now build both images using the following commands

Building the Frontend Image:

![WhatsApp Image 2024-04-24 at 11 39 56_4f436f19](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/4561f7b9-34e7-4736-8b7d-605404f82631)

Building the Backend Image:

![WhatsApp Image 2024-04-24 at 11 40 10_c4920476](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/149c0dcc-a10a-448c-9e5d-4d0cf64cad13)

Step 6: Run MySQL docker container
-
```
docker run -d --name puja_mysql_db --network Docker_Assignment -p 3307:3306 -e MYSQL_ROOT_PASSWORD=<password> mysql:8.0
```

Creating a database and tables inside the mysql container
```
docker exec -it puja_mysql_db mysql -u root -p
```

Then you will be asked for password which is your_password. After that enter the following SQL queries in order to create a new Database.

![WhatsApp Image 2024-04-24 at 11 54 19_928b7f43](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/ea7cd6e6-7dcf-42f2-97ad-1021244b2407)
![WhatsApp Image 2024-04-24 at 11 46 55_b7362528](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/d27d6b9d-7f3e-4641-bf02-1f9c64ee4467)
![WhatsApp Image 2024-04-24 at 11 56 23_3e12a57e](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/ef0048e8-d4c2-47b9-943a-95707e7b524a)

Part 3: Running the application
--
step 7: Building the containers
-
To build all three containers use this command:

1. Frontend React app:
   ```
   docker run -d --name puja_frontend --network Docker_Assignment -p 3000:3000 frontend_image_21BCP446D
   ```
3. Backend NodeJS Express server :
   ```
   docker run -d --name puja_backend --network Docker_Assignment -p 5000:5000 backend_image_21BCP446D
   ```
5. MySQL Server:
   ```
   docker run -d --name puja_mysql_db --network Docker_Asignment -p 3307:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:8.0
   ```
![WhatsApp Image 2024-04-24 at 11 51 48_81fab397](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/f61827e5-dedf-49fc-93f6-a8feb11cab36)
Step 8: Open in Browser
-
Open http://localhost:3000 to see the Reacjs App and http://localhost:5000/students to see the API response from the express server.
![image](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/625f2b04-a24c-4455-99e8-c8e72a1747dc)
![WhatsApp Image 2024-04-25 at 00 32 33_c9e6fdb4](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/c6dd3e2c-0c63-4a16-bd25-90e49d5154c4)

To Check if the Application is running or not we can check that the data is comming to mysql or not by running the query in mysql container

![WhatsApp Image 2024-04-25 at 00 28 08_4084113b](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/e8b6aa8a-ebbf-42d6-ba55-62f809772a27)

```
select * from students;
```
![WhatsApp Image 2024-04-25 at 00 35 00_5afe96fd](https://github.com/pujamavadhiya/pujamavadhiya.github.io/assets/122553122/95cb8795-ef7f-4f3b-b983-d4fdc9ef9ba1)
