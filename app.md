# CMS Cloud Manager: App documentation

The CMS Cloud Manager app lets you create projects, choose options, and thanks to the connection to providers' APIs, obtain the YAML file to run with the CLI tool, or run it directly.

## Prerequisites

- Docker: Ensure Docker is installed and running on your system.
- Git: To clone the repository.
- (Optional) Docker Compose: If you plan to run multiple containers or use a Compose file.

## Installation

### Clone the Repository

Clone the repository to your local machine using Git:

```bash
git clone https://github.com/cmscloudmanager/app.git
cd app
```

### Review the Dockerfile

Open the `Dockerfile` provided in the repository to understand the environment setup and dependencies. This helps if you need to customize the image or troubleshoot issues.

### Build the Docker Image

Build the Docker image using the following command:

```bash
docker build -t cmscloudmanager/app .
```

This command tells Docker to build an image from the Dockerfile in the current directory and tag it as `cmscloudmanager/app`.

### Run the Docker Container

Once the image is built, run the container:

```bash
docker run -d -p 80:80 cmscloudmanager/app
```

- The `-d` flag runs the container in detached mode.
- The `-p 80:80` flag maps port 80 in the container to port 80 on your host machine (adjust these ports as needed).

### Verify the Application

After the container starts, open your browser and navigate to:

```
http://localhost
```

You should see the application running. If the port mapping or application entry point is different, adjust the URL accordingly.

### (Optional) Using Docker Compose

If the project includes a `docker-compose.yml` file, you can use Docker Compose to manage the container(s). Simply run:

```bash
docker-compose up -d
```

This command builds and starts the containers as defined in the `docker-compose.yml` file.

### Managing the Container

- **Check Running Containers:**

  ```bash
  docker ps
  ```

- **View Logs:**

  ```bash
  docker logs <container_id>
  ```

- **Stop the Container:**

  ```bash
  docker stop <container_id>
  ```

Replace `<container_id>` with the actual container ID from the `docker ps` output.
