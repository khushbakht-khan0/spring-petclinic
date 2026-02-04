# Spring PetClinic - Containerization & Static Analysis

This repository contains the containerized version of the Spring PetClinic application, along with instructions for deploying it using Docker and performing static code analysis using SonarQube.

## Project Overview
* **Application:** Spring PetClinic (Java/Spring Boot)
* **Goal:** Dockerize the legacy application and audit code quality.
* **Tools Used:** Docker, Maven, SonarQube

---

## Part 1: Docker Execution Steps

Follow these steps to build and run the application container.

### 1. Build the Docker Image
Navigate to the project root directory (where the `Dockerfile` is located) and run:
```bash
docker build -t petclinic-app .

```

### 2. Run the Container

Start the application container on port 8080:

```bash
docker run -p 8080:8080 petclinic-app

```

### 3. Verify Deployment

Open your browser and navigate to:
[http://localhost:8080](https://www.google.com/search?q=http://localhost:8080)
You should see the Spring PetClinic welcome page.

---

## Part 2: SonarQube Analysis Steps

Follow these steps to perform static code analysis.

### 1. Start SonarQube Server

Pull and run the official SonarQube Docker image:

```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube:lts

```

* Access the dashboard at: [http://localhost:9000](https://www.google.com/search?q=http://localhost:9000)
* **Default Login:** `admin` / `admin` (You will be prompted to change the password).

### 2. Create Project & Token

1. Log in to SonarQube.
2. Click **Create Project** > **Manually**.
3. **Project Key:** `spring-petclinic1`
4. **Display Name:** `Spring Petclinic1`
5. Select **Locally** analysis method and generate a **Project Token**.

### 3. Run the Analysis

Execute the SonarScanner using the Maven wrapper. Replace `<YOUR_TOKEN>` with the token generated in the previous step.

**Windows Command:**

```cmd
mvnw clean verify sonar:sonar -DskipTests ^
  -Dsonar.projectKey=spring-petclinic1 ^
  -Dsonar.host.url=http://localhost:9000 ^
  -Dsonar.login=<YOUR_TOKEN>

```

**Linux/Mac Command:**

```bash
./mvnw clean verify sonar:sonar -DskipTests \
  -Dsonar.projectKey=spring-petclinic1 \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<YOUR_TOKEN>

```

### 4. View Results

Once the build is successful, refresh the SonarQube dashboard at [http://localhost:9000](https://www.google.com/search?q=http://localhost:9000) to view code smells, technical debt, and quality gate status.

```

```