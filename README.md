
# Building a Simple Docker Project with MLflow and Streamlit

## Introduction:
This project serves as an educational guide for beginners to set up and run services using Docker and Docker Compose. It focuses on deploying two services:
1. **MLflow**: An open-source platform to manage the machine learning lifecycle.
2. **Streamlit**: A simple framework for building interactive web applications for data projects.

---

## Objectives:
- Introduce beginners to the fundamentals of Docker and Docker Compose.
- Create separate `Dockerfile`s for MLflow and Streamlit services.
- Launch both services using a `docker-compose.yml` file.

---

## Setup:

### Prerequisites:
- **Docker** installed.
- **Docker Compose** installed.
- Basic knowledge of Python.

---

## Project Steps:

### 1. Create a Dockerfile for Each Service:

#### Dockerfile for MLflow:
```dockerfile
FROM python:3.9-slim

# Install the MLflow library
RUN pip install mlflow

# Set the working directory
WORKDIR /app

# Expose the port
EXPOSE 5001

# Default command to run the MLflow server
CMD ["mlflow", "server", "--host", "0.0.0.0", "--port", "5001"]
```

#### Dockerfile for Streamlit:
```dockerfile
FROM python:3.9-slim

# Install the Streamlit library
RUN pip install streamlit

# Copy the application file
COPY app.py /app/app.py

# Set the working directory
WORKDIR /app

# Expose the port
EXPOSE 8501

# Default command to run the Streamlit app
CMD ["streamlit", "run", "app.py", "--server.address=0.0.0.0", "--server.port=8501"]
```

### 2. Prepare the `app.py` File for Streamlit:
```python
# app.py
import streamlit as st

st.title("Simple Streamlit Application")
st.write("Welcome to the MLflow integration interface!")
```

### 3. Write the `docker-compose.yml` File:
```yaml
services:
  mlflow:
    build:
      context: .
      dockerfile: Dockerfile.mlflow
    ports:
      - "5001:5001"

  streamlit:
    build:
      context: .
      dockerfile: Dockerfile.streamlit
    ports:
      - "8501:8501"
```

---

## Running the Project:

### 1. Build and Run the Containers:
Run the following command:
```bash
docker-compose up --build
```

### 2. Access the Services:
- **MLflow**: [http://localhost:5001](http://localhost:5001)
- **Streamlit**: [http://localhost:8501](http://localhost:8501)

---

## Educational Takeaways:

1. **Dockerfile Basics:**
   - Define the base image (e.g., `python:3.9-slim`).
   - Install required libraries using `pip install`.
   - Configure ports using `EXPOSE`.
   - Specify default commands with `CMD`.

2. **Docker Compose Essentials:**
   - Combine multiple services into one project.
   - Define port mappings and network connections between containers.

---

## Future Enhancements:
- Connect MLflow to a database like MySQL.
- Add a third service such as an API interface using FastAPI.
- Enhance the Streamlit interface to enable interaction with MLflow functionalities.

---

## Conclusion:
This project provides a foundational understanding of deploying a multi-service application using Docker. It offers a stepping stone for beginners to build more complex and integrated projects in the future.
