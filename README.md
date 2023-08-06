# Installing Grafana on Docker

This guide will walk you through the steps to install Grafana on Docker. Docker allows you to run Grafana in a container, making it easy to set up and manage the application without worrying about complex dependencies.

## Prerequisites

Before you begin, ensure that you have the following installed on your system:

- Docker: Make sure Docker is installed and running on your machine. You can download it from the official website: [Docker](https://www.docker.com/get-started).

## Installation Steps

Follow these steps to install Grafana using Docker:

### 1. Pull Grafana Docker Image

Open your terminal or command prompt and enter the following command to pull the official Grafana Docker image from Docker Hub:

```bash
docker pull grafana/grafana
```

### 2. Run Grafana Container

Once the image is downloaded, run the Grafana container using the following command:

```bash
docker run -d -p 3000:3000 --name grafana grafana/grafana
```

Explanation of the command options:
- `-d`: Detached mode, the container runs in the background.
- `-p 3000:3000`: Maps port 3000 of the container to port 3000 on the host. Grafana web interface is accessible through `http://localhost:3000`.
- `--name grafana`: Assigns the name "grafana" to the container.

To add automatic restart functionality to the Grafana container, you can use the `--restart` option when running the container. This option allows you to define when and under what conditions Docker should automatically restart the container if it exits unexpectedly.

Here are the modified steps to include automatic restart functionality:

### Optional: Run Grafana Container with Automatic Restart

Use the following command to run the Grafana container with automatic restart:

```bash
docker run -d -p 3000:3000 --name grafana --restart unless-stopped -v grafana-storage:/var/lib/grafana grafana/grafana
```

Explanation of the additional command option:
- `--restart unless-stopped`: This option tells Docker to restart the container unless it is explicitly stopped by the user. It ensures that if your system reboots or the container crashes, Docker will automatically restart the Grafana container.

With this modification, your Grafana container will automatically restart whenever the Docker daemon is running, ensuring the service remains available even after system reboots or container failures.

Remember that Grafana will still retain its data and configuration in the `grafana-storage` volume as per the previous steps.

Now you have a resilient Grafana setup with automatic restart functionality in case of unexpected failures.

### 3. Access Grafana

Now that Grafana is running, open your web browser and navigate to `http://localhost:3000`. You should see the Grafana login page.

- Default username: `admin`
- Default password: `admin`

**Note**: It's highly recommended to change the default admin password after logging in for the first time.

### 4. Configuration and Persistence (Optional)

By default, Grafana's data and configuration are stored inside the Docker container. If you want to persist the data and make custom configuration changes, it's recommended to create a Docker volume to store Grafana data outside the container.

#### Create a Docker Volume

Run the following command to create a Docker volume:

```bash
docker volume create grafana-storage
```

#### Run Grafana Container with Volume

Use the following command to run the Grafana container with the volume:

```bash
docker run -d -p 3000:3000 --name grafana -v grafana-storage:/var/lib/grafana grafana/grafana
```

This will ensure that Grafana data is stored in the `grafana-storage` volume on your host system.

### 5. Stopping Grafana

To stop the Grafana container, use the following command:

```bash
docker stop grafana
```

### 6. Starting Grafana

To start the Grafana container again, use the following command:

```bash
docker start grafana
```

### 7. Removing Grafana Container

If you want to remove the Grafana container, use the following command:

```bash
docker rm grafana
```

### 8. Removing Grafana Image

To remove the Grafana Docker image from your system, use the following command:

```bash
docker rmi grafana/grafana
```

## Congratulations!

You have successfully installed Grafana on Docker. Now, you can start exploring Grafana's powerful features and visualize your data.

For more information and documentation about Grafana, visit the official website: [Grafana Documentation](https://grafana.com/docs/).

---
*Please note that this guide assumes you are using a system compatible with Docker. Make sure you have the necessary permissions to execute Docker commands.*
