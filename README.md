Certainly! Here is the entire `README.md` content in a single continuous format for easy copy-pasting:

```markdown
# yifan_ml_docker_lite

A lightweight Dockerfile for basic machine learning purposes, designed to set up a development environment with essential tools and libraries.

## Getting Started

These instructions will help you set up and run the Docker environment on your local machine.

### Prerequisites

Before you begin, ensure you have the following installed on your machine:

- [Docker](https://docs.docker.com/get-docker/)

### Building the Docker Image

1. **Clone the Repository**

   First, clone this repository to your local machine using Git:

   ```bash
   git clone https://github.com/yourusername/ml-nlp-docker.git
   cd ml-nlp-docker
   ```

2. **Create a `workdir` Directory**

   Create a directory named `workdir` in the root of your cloned repository. This directory will be mounted to the Docker container and will contain your project files.

   ```bash
   mkdir workdir
   ```

3. **Build the Docker Image**

   Run the following command to build the Docker image:

   ```bash
   docker build -t ml-environment .
   ```

### Running the Docker Container

After building the image, you can run the Docker container using the following command:

```bash
docker run -p 8888:8888 -v $(pwd)/workdir:/app ml-environment
```

This command does the following:
- `-p 8888:8888`: Maps port 8888 on your local machine to port 8888 on the container, allowing you to access JupyterLab.
- `-v $(pwd)/workdir:/app`: Mounts the `workdir` directory in your current location to `/app` in the container, so you can easily work with your project files.

### Accessing JupyterLab

Once the container is running, you can access JupyterLab by opening your web browser and navigating to:

```
http://localhost:8888
```

JupyterLab is configured to not require a token for access.

### Installed Packages

The Docker image comes with the following key packages pre-installed:

- jupyter = "*"
- python-dateutil = "2.9.0"
- requests = "2.32.2"
- matplotlib = "3.9.0"
- pandas = "2.2.2"
- numpy = "1.26.4"
- joblib = "1.4.2"
- scipy = "1.12.0"
- seaborn = "0.13.2"
- scikit-learn = "1.5.0"
- threadpoolctl = "3.5.0"
- pymatgen = "2024.5.1"
- mp-api = "0.41.2"
- japanize-matplotlib = "1.1.3"
- pycaret = "3.3.2"

### Customizing the Environment

If you need additional packages, you can modify the `Pipfile` and rebuild the Docker image:

1. Add the package to the `[packages]` section in the `Pipfile`.
2. Rebuild the Docker image:

   ```bash
   docker build -t ml-environment .
   ```

### Rebuilding the Docker Image

When you need to rebuild the Docker image, it's a good practice to stop and remove the old container and image first. Here is a script to automate this process:

```bash
#!/bin/bash

# Stop the running container
docker stop ml-nlp-container

# Remove the container
docker rm ml-nlp-container

# Remove the old image
docker rmi ml-environment

# Rebuild the Docker image
docker build -t ml-environment .

# Run the new container
docker run -d --name ml-nlp-container -p 8888:8888 -v $(pwd)/workdir:/app ml-environment
```

Save this script as `rebuild.sh` and run it with:

```bash
chmod +x rebuild.sh
./rebuild.sh
```

This script automates the process of stopping, removing, rebuilding, and running the Docker container, ensuring a clean setup each time you rebuild the image.

### Contributing

Feel free to open issues or submit pull requests if you have any improvements or bug fixes.

### License

This project is licensed under the MIT License.
