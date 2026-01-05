# 🚀 CI/CD Pipeline Automation Using Jenkins, Docker, and Apache Tomcat (Single Server)

## 📌 Project Overview
This project demonstrates a **complete CI/CD pipeline** for deploying a **Java web application** using **Jenkins, Docker, and Apache Tomcat** on a **single Linux server**.

The goal is to automate the process of:
- Pulling source code from Git
- Building the application using Maven
- Deploying the WAR file to Apache Tomcat running inside a Docker container

This setup reflects a **real-world DevOps workflow** and is suitable for **learning, interviews, and hands-on practice**.

---

## 🏗️ Architecture (Single Server)
```text
Developer → GitHub
              ↓
          Jenkins
        (Build + Package)
              ↓
            Maven
          (WAR File)
              ↓
        Docker Container
          (Tomcat)
              ↓
        Web Application
```
🛠️ Tools & Technologies Used
Linux (Ubuntu)

Java 11

Git

Apache Maven

Jenkins

Docker

Apache Tomcat (Dockerized)

📂 Project Structure
```text
Copy code
jenkins-docker-tomcat-ci-cd/
├── README.md
├── Jenkinsfile 
├── pom.xml
├── src/
│   └── main/
│       └── webapp/
└── screenshots/
```
🔧 Prerequisites
One Linux server (Ubuntu 20.04 / 22.04)

User with sudo access

Internet connectivity

🔹 Step-by-Step Setup (Linux Commands)
STEP 1️⃣ Update System
```text
Copy code
sudo apt update -y
sudo apt upgrade -y
```
STEP 2️⃣ Install Java
```text
Copy code
sudo apt install openjdk-11-jdk -y
java -version
```
STEP 3️⃣ Install Docker
```text
Copy code
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```
Add current user to Docker group:

```text
Copy code
sudo usermod -aG docker $USER
newgrp docker
```
Verify Docker:

```text
Copy code
docker run hello-world
```
STEP 4️⃣ Install Jenkins
```text
Copy code
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update -y
sudo apt install jenkins -y
```
Start Jenkins:

```text
Copy code
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
Access Jenkins:

```text
Copy code
http://SERVER_IP:8080
```
Get admin password:

```text
Copy code
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
STEP 5️⃣ Install Maven
```text
Copy code
sudo apt install maven -y
mvn -version
```
STEP 6️⃣ Install Git
```text
Copy code
sudo apt install git -y
git --version
```
STEP 7️⃣ Run Tomcat Using Docker
```text
Copy code
docker pull tomcat:9.0
```
Run Tomcat container:

```text
Copy code
docker run -d \
--name tomcat \
-p 8081:8080 \
tomcat:9.0
```
Verify:

```text
docker ps
```
Access Tomcat:

```text
http://SERVER_IP:8081
```
⚙️ Jenkins Job Configuration
# Job Type
-  Freestyle Project

# Source Code Management
- it Repository URL

# Build Step – Maven
```text
mvn clean package
```
# Deploy WAR to Tomcat (Docker)
```text
docker cp target/*.war tomcat:/usr/local/tomcat/webapps/
docker restart tomcat
```
🌐 Application Access
```text
http://SERVER_IP:8081/<application-name>
```
🔄 CI/CD Workflow Summary
- Developer pushes code to GitHub

- Jenkins pulls source code

- Maven builds WAR file

- WAR is deployed to Tomcat Docker container

- Application is live

📌 Key DevOps Concepts Demonstrated
- CI/CD Pipeline Automation

- Jenkins Build Automation

- Docker Containerization

- Tomcat Application Deployment

- Single Server DevOps Architecture

🧠 Interview Explanation (Short)
This project implements a CI/CD pipeline using Jenkins to automate the build and deployment of a Java application. Maven handles packaging, Docker provides containerization, and Apache Tomcat runs the application, all hosted on a single Linux server.

✅ Future Enhancements
- Jenkins Pipeline (Jenkinsfile)

- Dockerfile for custom image

- GitHub Webhook integration

- Blue-Green deployment

- Multi-server architecture

📎 Author
Vignesh Reddy
DevOps | CI/CD | Docker | Jenkins
