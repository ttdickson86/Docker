# Docker And Docker-Compose

**Project Description**  

This project is a multi-container application built with **Docker** and **Docker Compose**, designed to simplify the development, testing, and deployment of modern web applications. It leverages containerization to ensure consistency across environments, enabling seamless collaboration and efficient resource management.  

The project includes a `docker-compose.yml` file that defines the services, networks, and volumes required for your application. It is ideal for applications that require multiple dependencies (e.g., web servers, databases, message queues) to function together. Whether you're building a simple static site, a microservice, or a complex backend system, this project provides a streamlined workflow for setting up and managing your application.  

Key features:  
- **Containerized services**: All components are encapsulated in Docker containers for isolation and portability.  
- **Easy setup**: A single `docker-compose up` command starts the entire application, including dependencies.  
- **Scalable architecture**: Designed to work with Docker’s ecosystem for easy scaling and maintenance.  
- **Environment consistency**: Ensures the same environment across development, testing, and production.  

To get started:  
1. Install Docker and Docker Compose on your system.  
2. Clone this repository and navigate to the project directory.  
3. Run `docker-compose up` to launch the application.  
4. Explore the `docker-compose.yml` file to customize services, networks, and volumes as needed.  

This project is a great starting point for developers looking to adopt containerization and streamline their workflow with Docker and Docker Compose. Let me know if you'd like help tailoring it to your specific use case! 🚀



# Introduction to Docker and Docker Compose

## What is Docker?

**Docker** is a platform that enables developers to package, ship, and run applications in **containers**—lightweight, isolated environments that include everything needed to run an application. Containers ensure consistency across different environments, from development to production. By leveraging Docker, developers can streamline the deployment process, improve collaboration, and simplify system management.

## What is Docker Compose?

**Docker Compose** is a tool that extends Docker’s capabilities by allowing you to define and manage **multi-container applications** using a single YAML file. It simplifies the process of starting, stopping, and scaling multiple Docker containers that work together as a single service. This is particularly useful for complex applications that require multiple services (e.g., databases, web servers, and message brokers) to function together.

## Installing Docker Engine on Debian

This guide explains how to install **Docker Engine** on a **Debian-based system**. Docker is a prerequisite for using Docker Compose.

### Prerequisites
- A Debian system (e.g., Debian 11 or later).
- Administrative privileges (sudo access).

### Step-by-Step Installation

1. **Update the package list**:
   ```bash
   sudo apt update
   ```

2. **Install required packages**:
   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common
   ```

3. **Add the Docker GPG key**:
   ```bash
   curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

4. **Add the Docker repository**:
   ```bash
   echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

5. **Update the package list again**:
   ```bash
   sudo apt update
   ```

6. **Install Docker Engine**:
   ```bash
   sudo apt install docker-ce docker-ce-cli containerd.io
   ```

7. **Verify the installation**:
   ```bash
   sudo docker info
   ```

   If the installation is successful, you’ll see details about Docker’s environment.

8. **Start and enable Docker service**:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

### Docker Compose

After installing Docker Engine, **Docker Compose** is included by default. You can verify its installation by running:
```bash
docker-compose --version
```

If the command returns a version number, Docker Compose is installed and ready to use.

---

## Next Steps

This repository is designed to help you get started with Docker and Docker Compose. Follow the instructions in this README to install Docker on Debian, then explore the `docker-compose.yml` file in this project to see how multi-container applications are defined and managed.


To run a sample application using **Docker Compose** after installing Docker on Debian, follow these steps:

---

### **Step 1: Navigate to the Project Directory**
Ensure you are in the root directory of your GitHub repository (where the `docker-compose.yml` file is located):

```bash
cd /path/to/your/repo
```

---

### **Step 2: Check the `docker-compose.yml` File**
This file defines the services, networks, and volumes for your application. For example, a simple web app might look like this:

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
```

If the file is missing, you can create one based on your application's needs.

---

### **Step 3: Run the Application**
Use the following command to start the application:

```bash
docker-compose up
```

- **`docker-compose up`**:
  - Builds and starts the services defined in `docker-compose.yml` (if needed).
  - Runs the containers in **detached mode** (background).
  - Displays logs in the terminal by default.

---

### **Step 4: Optional: Run in Detached Mode**
If you want the containers to run in the background:

```bash
docker-compose up -d
```

---

### **Step 5: Stop the Application**
To stop the containers:

```bash
docker-compose down
```

- **`docker-compose down`**:
  - Stops and removes the containers.
  - Removes the networks and volumes (if not using `--volumes`).

To remove volumes as well:

```bash
docker-compose down --volumes
```

---

### **Step 6: View Logs**
If you need to debug or monitor the application:

```bash
docker-compose logs -f
```

- `-f` keeps the logs running in real-time.

---

### **Example: Run a Simple Nginx Web Server**
If your `docker-compose.yml` includes an Nginx service, the command:

```bash
docker-compose up
```

will start an Nginx server, serving files from the `html` directory in your project.

---

### **Notes**
- If your project uses a `Dockerfile`, Docker Compose will automatically build the image when you run `docker-compose up`.
- You can customize the `docker-compose.yml` file to include multiple services (e.g., a web app, database, and Redis).
- Always check the `docker-compose.yml` file for specific configurations (ports, environment variables, etc.).

---

By following these steps, you can quickly test and deploy your application using Docker Compose. Let me know if you need help customizing the `docker-compose.yml` file! 🚀


## To customize the `docker-compose.yml` file for your specific application, you need to define the services, networks, and volumes that make up your application. Below is a step-by-step guide to help you customize the file based on your needs:

---

### **1. Understand the Structure of `docker-compose.yml`**
A `docker-compose.yml` file is a YAML file that defines the services, networks, and volumes for your application. Here is a basic structure:

```yaml
version: '3'
services:
  <service-name>:
    image: <image-name>
    ports:
      - "80:80"
    environment:
      - KEY=VALUE
    volumes:
      - ./data:/app/data
    depends_on:
      - <dependent-service>
networks:
  <network-name>:
    driver: bridge
volumes:
  <volume-name>:
    driver: local
```

---

### **2. Customize the File for Your Application**

#### **a. Define the Service**
Each service represents a container in your application. For example, if you're running a web application:

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    environment:
      - ENV_VAR=your-value
```

- **`image`**: The Docker image to use (e.g., `nginx`, `your-username/your-image`).
- **`ports`**: Map host ports to container ports (e.g., `80:80`).
- **`volumes`**: Mount host directories to the container (e.g., `./html:/usr/share/nginx/html`).
- **`environment`**: Set environment variables for the container.

#### **b. Add Dependencies**
If one service depends on another (e.g., a web app depends on a database), use `depends_on`:

```yaml
  db:
    image: postgres
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=secret
    ports:
      - "5432:5432"

  web:
    image: your-username/web-app
    depends_on:
      - db
    ports:
      - "80:80"
```

#### **c. Define Networks**
If your services need to communicate with each other, define a shared network:

```yaml
networks:
  app-network:
    driver: bridge
```

Then, reference the network in your service:

```yaml
  web:
    networks:
      - app-network
```

#### **d. Define Volumes**
For persistent data, define a volume:

```yaml
volumes:
  data-volume:
    driver: local
```

Mount it in your service:

```yaml
  db:
    volumes:
      - data-volume:/var/lib/postgresql/data
```

---

### **3. Example: Customizing for a Web App with a Database**

Here’s a full example for a web app with a PostgreSQL database:

```yaml
version: '3'
services:
  db:
    image: postgres
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=secret
    ports:
      - "5432:5432"
    volumes:
      - db-data:/var/lib/postgresql/data

  web:
    image: your-username/web-app
    ports:
      - "80:80"
    depends_on:
      - db
    environment:
      - DB_HOST=db
      - DB_USER=admin
      - DB_PASSWORD=secret
    volumes:
      - ./app:/app
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  db-data:
    driver: local
```

---

### **4. Run Your Customized Application**

After customizing the file, run the following command to start your services:

```bash
docker-compose up
```

- **`docker-compose up`**: Builds and starts the services defined in the file.
- **`docker-compose down`**: Stops and removes the services, networks, and volumes.

---

### **5. Tips for Customization**
- **Use `build` if you have a `Dockerfile`**:
  ```yaml
  web:
    build: .
    ports:
      - "80:80"
  ```
- **Check the Docker Compose version**:
  ```yaml
  version: '3.8'
  ```
  Ensure this matches your Docker Compose version.
- **Use environment variables** for configuration:
  ```yaml
  environment:
    - DB_PASSWORD=${DB_PASSWORD}
  ```

---

### **6. Test and Debug**
- Use `docker-compose logs` to view logs:
  ```bash
  docker-compose logs -f
  ```
- Use `docker-compose ps` to check the status of services:
  ```bash
  docker-compose ps
  ```

---

### **7. Save and Share**
Once customized, the `docker-compose.yml` file is ready to be used for deployment, testing, or sharing with your team.

---

By customizing the `docker-compose.yml` file, you can tailor your application’s environment to fit your needs, ensuring consistency across development, testing, and production environments. Let me know if you need help with specific services or configurations! 🚀


## FOLLOW UP

How do I add a custom service to the docker-compose.yml file?

Can you explain how to set environment variables in the docker-compose.yml?

What are best practices for scaling the application with Docker Compose?

How can I integrate a database with my project using Docker Compose?

What tools can I use to monitor the application after deployment?


## To add a **custom service** to your `docker-compose.yml` file, follow these steps:

---

### **1. Understand the Structure**
The `docker-compose.yml` file defines services, networks, and volumes. To add a new service, place it under the `services` key. Here's a basic template:

```yaml
version: '3'
services:
  <service-name>:
    image: <image-name>
    ports:
      - "80:80"
    environment:
      - KEY=VALUE
    volumes:
      - ./data:/app/data
    depends_on:
      - <dependent-service>
networks:
  app-network:
    driver: bridge
volumes:
  data-volume:
    driver: local
```

---

### **2. Add a Custom Service**
Let’s say you want to add a **custom web service** using a specific Docker image. Here’s an example:

```yaml
version: '3'
services:
  # Existing services (e.g., nginx, database)
  web:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html

  # New custom service
  custom-service:
    image: your-username/custom-service
    ports:
      - "3000:3000"
    environment:
      - ENV_VAR=custom-value
    volumes:
      - ./custom-data:/app/data
    depends_on:
      - web
```

---

### **3. Key Parameters for a Custom Service**
- **`image`**: The Docker image to use. You can use a public image (e.g., `nginx`, `postgres`) or a private image (e.g., `your-username/custom-service`).
- **`ports`**: Map host ports to container ports (e.g., `3000:3000`).
- **`environment`**: Set environment variables for the container.
- **`volumes`**: Mount host directories or volumes to the container.
- **`depends_on`**: Define dependencies (e.g., a service that must start before your custom service).

---

### **4. Example: Add a Redis Service**
If you want to add a Redis service for caching, the `docker-compose.yml` would look like this:

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html

  redis:
    image: redis
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data

volumes:
  redis-data:
    driver: local
```

---

### **5. Run the Updated Compose File**
After adding your custom service, run:

```bash
docker-compose up
```

- This will start all services, including your new one.
- If you want to run in the background:
  ```bash
  docker-compose up -d
  ```

---

### **6. Stop or Remove the Service**
To stop and remove the service:

```bash
docker-compose down
```

- Use `--volumes` to remove data volumes:
  ```bash
  docker-compose down --volumes
  ```

---

### **7. Customize Further**
You can add more services, networks, or volumes as needed. For example, if your custom service depends on a database:

```yaml
services:
  custom-service:
    depends_on:
      - db
```

---

### **Tips**
- Ensure the `version` line matches your Docker Compose version (e.g., `version: '3'`).
- Use `build:` if you’re using a `Dockerfile` for the service.
- Check for syntax errors (YAML is sensitive to indentation).

---

By adding a custom service to your `docker-compose.yml`, you can easily integrate new components into your application workflow. Let me know if you need help with specific configurations! 🚀



## To set **environment variables** in a `docker-compose.yml` file, you can use two main approaches: **inline variables** (directly in the YAML) or **external files** (via `env_file`). Below is a detailed explanation of both methods:

---

### **1. Inline Environment Variables**
You can define environment variables directly in the `environment` key of a service. This is useful for simple or short-lived variables.

#### **Example:**
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
    environment:
      - KEY1=VALUE1
      - KEY2=VALUE2
```

- **Explanation**:
  - `KEY1=VALUE1` and `KEY2=VALUE2` are environment variables passed to the `nginx` container.
  - These variables are available to the container's processes, such
  as in a script or command: `${KEY1}`.

---

### **2. External Environment Files (`env_file`)**

You can load environment variables from a `.env` file using the `env_file` key. This is useful for managing secrets or large sets of variables.

#### **Step 1: Create a `.env` file**
```env
KEY1=VALUE1
KEY2=VALUE2
```

#### **Step 2: Reference the file in `docker-compose.yml`**
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
    env_file:
      - .env
```

- **Explanation**:
  - The `env_file` directive tells Docker Compose to load variables from the `.env` file.
  - You can also specify multiple files: `env_file: - .env - .env2`.

#### **Optional: Override Variables**
If you want to override a variable from the file, use the `override` keyword:
```yaml
env_file:
  - .env
  - override:
      KEY1=OVERRIDDEN_VALUE
```

---

### **3. Best Practices**
- **Security**: Avoid exposing sensitive variables (e.g., passwords) in version-controlled repositories. Use `env_file` or secret management tools instead.
- **Consistency**: Use `env_file` for shared variables across multiple services.
- **Debugging**: Use `docker-compose env` to list all environment variables for a service.

---

### **4. Accessing Variables in the Container**
Environment variables are accessible in the container via:
```bash
echo $KEY1
```
Or in scripts:
```bash
my_script.sh "${KEY1}"
```

---

### **5. Example with a Custom Service**
```yaml
version: '3'
services:
  myapp:
    image: myapp
    ports:
      - "8080:8080"
    environment:
      - ENV_VAR=custom-value
    env_file:
      - .env
```

---

By using these methods, you can dynamically configure your containers with environment variables, making your application more flexible and secure. Let me know if you need help with specific use cases! 🚀