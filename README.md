# ☁️ Hello Cloud — Flask, Docker & Jenkins CI/CD

A modern, responsive landing page built with **Python and Flask**, showcasing a hands-on DevOps learning project focused on containerization and CI/CD concepts.

The project transforms a basic Flask `Hello, World!` application into a polished web interface that presents the software delivery workflow from source code to deployment.

## 🚀 Project Overview

**Hello Cloud** is a lightweight Flask web application created as part of my practical DevOps learning journey. It demonstrates how a simple Python application can serve a professional-looking frontend and fit into a container-based delivery workflow.

### ✨ Features

- **Modern UI:** Dark theme, gradient accents, responsive layout, and custom CSS styling.
- **Python & Flask:** Lightweight web application with server-side routing.
- **Docker:** Containerization for consistent application packaging and execution.
- **Jenkins:** CI/CD pipeline integration for practicing automated build and deployment workflows.
- **Health Endpoint:** A `/health` route returns a JSON response to help verify application availability.
- **Responsive Design:** Layout adapts to desktop and mobile screens.
- **No Frontend Framework Required:** The interface uses HTML and CSS served directly by Flask.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application logic |
| Flask | Web framework and routing |
| HTML5 | Page structure |
| CSS3 | Styling and responsive layout |
| Docker | Application containerization |
| Jenkins | CI/CD pipeline automation |
| Git & GitHub | Version control and source management |

## 🏗️ Architecture

```text
Developer
    |
    v
GitHub Repository
    |
    v
Jenkins Pipeline
    |
    v
Docker Image Build
    |
    v
Application Container
    |
    v
Flask Web Application
    |
    v
Browser — Port 5000
```

*The diagram represents the intended workflow; individual stages depend on the configured Jenkins pipeline.*

## 📁 Project Structure

```text
nti-python-jenkins/
├── hello.py
├── Dockerfile
├── requirements.txt
├── Jenkinsfile
└── README.md
```

The exact files may vary depending on the repository configuration.

## ⚙️ Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/drift3/nti-python-jenkins.git
cd nti-python-jenkins
```

### 2. Create a virtual environment (optional)

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

On Linux:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

The requirements file should include:

```text
Flask
```

### 4. Start the application

```bash
python hello.py
```

Open the following URLs:

- **Web application:** http://localhost:5000
- **Health check:** http://localhost:5000/health

Expected health-check response:

```json
{
  "status": "ok",
  "application": "hello-cloud"
}
```

## 🐳 Run with Docker

Build the image using the Dockerfile in the repository:

```bash
docker build -t hello-cloud:latest .
```

Start a container:

```bash
docker run -d \
  --name hello-cloud \
  -p 5000:5000 \
  hello-cloud:latest
```

Open http://localhost:5000 to view the application.

Useful commands:

```bash
# List running containers
docker ps

# View application logs
docker logs hello-cloud

# Stop the container
docker stop hello-cloud

# Remove the container
docker rm hello-cloud
```

If a container already uses port `5000`, stop or remove it before starting the new one.

## 🔄 Jenkins CI/CD

The project can be integrated with a Jenkins pipeline to practice the software delivery lifecycle:

1. Retrieve the source code from GitHub.
2. Build a Docker image.
3. Run validation or health checks.
4. Replace the running application container with the updated version.

The actual pipeline stages depend on the `Jenkinsfile` configuration. A successful Jenkins build alone does not guarantee that the application has been deployed successfully; the running container and health endpoint should also be verified.

## 🧠 What I Learned

- Connecting a Python web application to a container-based workflow.
- Understanding the relationship between source code, Docker images, and running containers.
- Practicing Jenkins pipeline execution and application delivery.
- Using health endpoints to verify application availability.
- Improving the presentation of a technical project for documentation and portfolio purposes.

## 🎯 Future Improvements

- Add automated tests with `pytest`.
- Add linting and code-quality checks.
- Publish versioned Docker images to Docker Hub.
- Integrate automated health checks into Jenkins.
- Add deployment notifications and build status reporting.
- Explore Kubernetes deployment and monitoring.

## 👨‍💻 Author

**Ahmed Farouk**

DevOps & Cloud Engineering Learner | Python | Docker | Jenkins | Linux | AWS

This project is part of my continuous hands-on learning journey in DevOps and cloud-native technologies.

---

⭐ If you find this project useful, feel free to explore the repository and share feedback.
