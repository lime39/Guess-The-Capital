# Guess the Capital

## Overview

"Guess the Capital" is a simple yet engaging web-based quiz application that challenges users to guess the capital city of a country from four multiple-choice options. This project demonstrates how to containerize a web application using Docker and provides steps to deploy it on IBM Cloud's Code Engine or run it locally.

## Features

- **Multiple Choice Quiz**: Test your knowledge of world capitals.
- **Dockerized**: Easily deploy the application as a Docker container.
- **Cloud-Ready**: Deploy the containerized application on IBM Cloud's Code Engine.

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- **Docker**: [Install Docker](https://www.docker.com/get-started)
- **Git**: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Getting Started

### Cloning the Repository

First, clone the repository to your local machine:

```bash
git clone https://github.com/lime39/guess-the-capital.git
cd guess-capital
```
## Running the Application Locally

### Step 1: Build the Docker Image
Create a Docker image from the provided Dockerfile:

```bash
docker build -t guess-capital .
```

### Step 2: Run the Docker Container
Run the Docker container:

```bash
docker run -it -d -p 8080:80 guess-capital
```

### Step 3: Access the Application
Open your web browser and navigate to:

```bash
http://localhost:8080
```
You should now see the application running.

## Deploying to IBM Cloud
If you wish to deploy the application on IBM Cloud's Code Engine, follow these steps:

**Note:** You need to create an IBM Cloud account to push your Docker images to IBM Cloud’s container registry and deploy them using IBM Code Engine. If you already have an account, skip to step 2.

### Step 1: Create an IBM Cloud Namespace
1. **Log in to IBM Cloud:**
```bash
ibmcloud login
```
2. **Create a Namespace:**
```bash
ibmcloud cr namespace-add <your-namespace>
```
Replace `<your-namespace>` with your desired namespace name. This name should be unique within IBM Cloud. 

3. **Verify your Namespace:**
```bash
ibmcloud cr namespace-list
```
This command will list all the namespaces you have created, and you should see your new namespace in the list.

### Step 2: Tag the Docker Image
Tag your Docker image for IBM Cloud:

```bash
docker tag guess-capital us.icr.io/<your-namespace>/guess-capital
```

### Step 3: Push the Docker Image to IBM Cloud
Push the image to IBM Cloud's container registry:

```bash
docker push us.icr.io/<your-namespace>/guess-capital
```
### Step 4: Deploy on IBM Code Engine
Deploy the image using IBM Code Engine
```bash
ibmcloud ce application create --name guess-capital --image us.icr.io/<your-namespace>/guess-capital --registry-secret icr-secret --port 80
```
After deployment, you can access the application via the URL provided by IBM Cloud.

Example: https://guess-the-capital.1lesj25xh9ao.us-south.codeengine.appdomain.cloud/

## Project Structure
```bash
├── Dockerfile          # Dockerfile for building the container
├── favicon.ico         # Favicon for the application
├── index.html          # Main HTML file
├── script.js           # JavaScript for the application logic
├── style.css           # CSS for styling
└── data.json           # Data file containing the capitals and countries
```
