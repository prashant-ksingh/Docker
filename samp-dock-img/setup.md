# 🚀 Insurance Premium Prediction API - Docker Guide

This guide will help you set up and run the Insurance Premium Prediction API using Docker. No prior experience with Docker is required!

---

## 📋 Prerequisites

1.  **Install Docker:** Download and install [Docker Desktop](https://www.docker.com/products/docker-desktop).
2.  **Open Terminal:** Open your Command Prompt (CMD), PowerShell, or Terminal.
3.  **Navigate to Project:** Go to your project folder:
    ```bash
    cd D:\samp-dock-img
    ```

---

## 🛠️ Step 1: Building the Docker Image

The first step is to "package" your application into a Docker image. Think of an image as a template for your app.

**Run this command:**
```bash
docker build -t prksingh/insurance_prediction .
```

### What does this command do?
- `docker build`: Tells Docker to create a new image.
- `-t prksingh/insurance_prediction`: Tags your image using the format `username/project-name`. 
    - **`prksingh`**: This is usually your **Docker Hub username**.
    - **`insurance_prediction`**: This is the **project name** (you can name this whatever you like).
- `.`: Tells Docker that all the files it needs are in the current folder.

**Success Output:**
When finished, you will see a message like:
`naming to docker.io/prksingh/insurance_prediction:latest`

---

## 🏃 Step 2: Running the Application

Now that you have an image, you can "run" it to start your API.

**Run this command:**
```bash
docker run -p 8000:8000 prksingh/insurance_prediction
```

### What does this command do?
- `-p 8000:8000`: This is the most important part! It connects port 8000 on your computer to port 8000 inside the Docker container.
- `prksingh/insurance_prediction`: The name of the image you just built.

**Success Output:**
You should see:
`Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)`

---

## 🌐 Step 3: Using the API

Once the app is running, you can interact with it using your browser:

1.  **Home Page:** Go to [http://localhost:8000/](http://localhost:8000/)
    - You should see: `{"message": "Insurance Premium Prediction API"}`
2.  **Health Check:** Go to [http://localhost:8000/health](http://localhost:8000/health)
3.  **Interactive Documentation:** Go to [http://localhost:8000/docs](http://localhost:8000/docs)
    - This is the "Swagger" UI where you can test the API manually.

---

## 🧪 Step 4: Testing a Prediction

To test if the model is working, you can send a "POST" request. 

**Using the Swagger UI (/docs):**
1. Click on the **POST /predict** button.
2. Click **"Try it out"**.
3. Use the following example data:
```json
{
  "age": 30,
  "weight": 75,
  "height": 1.75,
  "income_lpa": 5.5,
  "smoker": false,
  "city": "Mumbai",
  "occupation": "private_job"
}
```
4. Click **Execute**.

---

## 📤 Step 5: Pushing to Docker Hub

If you want to share your image or deploy it to a server, you can push it to Docker Hub.

### 1. Login to Docker Hub
Run this command and enter your Docker Hub password/token when prompted:
```bash
docker login
```

### 2. Push your image
Use the same name you used during the build step:
```bash
docker push prksingh/insurance_prediction
```

*Note: Make sure `prksingh` matches your actual Docker Hub username, otherwise the push will fail.*

---

## 💡 Pro Tips
- **Stop the App:** Press `CTRL + C` in your terminal to stop the container.
- **Run in Background:** Add `-d` to the run command (e.g., `docker run -d -p 8000:8000 ...`) to run the app without keeping the terminal open.
- **Cleanup:** If you want to delete the image to save space: `docker rmi prksingh/insurance_prediction`.
