# Flask Application Deployment Guide

This guide walks through the steps to run and deploy a Flask application locally and on Google Cloud Run.

## Table of Contents

1. [Running the Application Locally](#running-the-application-locally)
2. [Building and Testing the Docker Image](#building-and-testing-the-docker-image)
3. [Deployment Steps](#deployment-steps)
4. [Implementing CI/CD](#implementing-ci-cd)
5. [Faced Errors](#faced-errors)

---

## 1. Running the Application Locally

To run the application in your local environment, you need to start the Flask server using the following command:

> `python app.py`

---

## 2. Building and Testing the Docker Image

Once you have a Dockerfile, you can build an image and then test it:

**Step 2.1: Building the Docker Image**

> `docker build -t my_flask_app .`

**Step 2.2: Running the Docker Container**

> `docker run -p 8080:8080 my_flask_app`

---

## 3. Deployment Steps

To deploy the Docker image to Google Cloud Run, follow these steps:

**Step 3.1: Configuring Docker with GCloud**

> `gcloud auth configure-docker`

**Step 3.2: Tagging the Docker Image**

Replace `[YOUR-PROJECT-ID]` with your Google Cloud project ID.

> `docker tag my_flask_app gcr.io/[YOUR-PROJECT-ID]/my_flask_app`

**Step 3.3: Pushing the Docker Image**

> `docker push gcr.io/[YOUR-PROJECT-ID]/my_flask_app`

**Step 3.4: Deploying to Google Cloud Run**

Replace `SERVICE_NAME`, `PROJECT_ID`, `IMAGE_NAME`, and `REGION_NAME` with your service name, project ID, image name, and region respectively. For example:

> `gcloud run deploy flask-app --image gcr.io/flask-app-2023-387823/my_flask_app --platform managed --region us-central1`

---

## 4. Implementing CI/CD

You can automate the build and deployment process with Google Cloud Build.

**Step 4.1: Creating a Build Trigger**

Create a build trigger as per the instructions provided [here](https://cloud.google.com/build/docs/automating-builds/create-manage-triggers).

**Step 4.2: Adding a cloudbuild.yaml File**

Add a `cloudbuild.yaml` file to your GitHub repository, which specifies the build steps. This file automates the following:

- Building a Docker image from your Dockerfile.
- Pushing the Docker image to the Google Container Registry.
- Deploying the Docker image to Google Cloud Run.

Replace `my-service` with your actual service name and `us-central1` with your desired region. The `$PROJECT_ID` will be automatically replaced by your GCP project ID.

---

---

## 5. Faced Errors

**Step 5.1: from flask import Flask error**
- Activate the environment
    - windows: > `.venv\Scripts\activate`
    - macOS/Linux $`. .venv/bin/activate`
Your shell prompt will change to show the name of the activated environment.
- Install Flask
    - `$ pip install Flask`

- `python -m flask run`

Please refer to the relevant documentation for more detailed steps and troubleshooting. If you encounter issues or have further questions, feel free to raise an issue in this repository.

Helpful Links
Cloud Build Logs
https://console.cloud.google.com/cloud-build/builds?_ga=2.14484660.2062548505.1685055387-541186574.1670604918&_gac=1.162001102.1685055996.Cj0KCQjwjryjBhD0ARIsAMLvnF8Kadh5r1uNcQIn4c_KN-lIMVPhHiKCX9nrzrIZvjbbiCoUAeeHaZIaAgWWEALw_wcB

particles.js configuration
https://github.com/VincentGarreau/particles.js/
1) add particles.js
2) particles.json
3) index.html
    - header
    - div
    - script
