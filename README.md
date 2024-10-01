
# yifan_ml_docker_lite

A lightweight Docker environment for basic machine learning, equipped with essential tools and libraries to facilitate development.

## Getting Started

These instructions will guide you through setting up and running the Docker environment on your local machine.

### Prerequisites

Before you start, ensure you have Docker installed on your machine. You can download and install Docker from [here](https://docs.docker.com/get-docker/).

### Building the Docker Image

1. **Clone the Repository**

   Clone this repository to your local machine. When you clone a GitHub repository using the git clone command, the folder that is created on your local system will have the same name as the repository by default.

   ```bash
   git clone https://github.com/azarashiyifan/yifan_ml_docker_lite.git
   cd yifan_ml_docker_lite
   ```

2. **Create a `workdir` Directory**

   In the root of your cloned repository, create a directory named `workdir`. This will be mounted to the Docker container and will contain your project files.

   ```bash
   mkdir workdir
   ```

3. **Build the Docker Image**

   Build your Docker image by running:

   ```bash
   docker build -t yifan_ml_docker_lite .
   ```

### Running the Docker Container

After building the image, run the Docker container with:

```bash
docker run -d --name yifan_ml_docker_lite_container -p 8888:8888 -v $(pwd)/workdir:/app yifan_ml_docker_lite
```

This command will:
- Map port 8888 on your local machine to port 8888 on the container, enabling access to JupyterLab.
- Mount the `workdir` directory at your current location to `/app` in the container, facilitating easy access to your project files.
- Name the container yifan_ml_docker_lite_container for consistency.

### Accessing JupyterLab

Access JupyterLab by navigating to the following URL in your web browser:

```
http://localhost:8888
```

JupyterLab is set up to not require a token for access.

### Installed Packages

The Docker image includes the following key packages pre-installed:

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
- shap = "0.46.0"

### Customizing the Environment

To add additional packages, modify the `Pipfile` and rebuild the Docker image:

1. Add your desired package to the `[packages]` section in the `Pipfile`.
2. Rebuild the Docker image by running:

   ```bash
   docker build -t yifan_ml_docker_lite .
   ```

### Rebuilding the Docker Image

Use the following script to rebuild your Docker image, ensuring a clean setup:

```bash
#!/bin/bash

# Stop the running container
docker stop yifan_ml_docker_lite_container

# Remove the container
docker rm yifan_ml_docker_lite_container

# Remove the old image
docker rmi yifan_ml_docker_lite

# Rebuild the Docker image
docker build -t yifan_ml_docker_lite .

# Run the new container
docker run -d --name yifan_ml_docker_lite_container -p 8888:8888 -v $(pwd)/workdir:/app yifan_ml_docker_lite
```

### Contributing

We welcome contributions! Feel free to open issues or submit pull requests with improvements or bug fixes.

### License

This project is licensed under the MIT License.
