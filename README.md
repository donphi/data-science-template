# Data Science Project Template

## Overview

This project template enables data scientists to use **Visual Studio Code** with a consistent and isolated Docker environment. It’s cross-platform, supporting **Windows**, **macOS**, and **Linux**—ideal for AI and data science work. With this setup, all dependencies are managed within Docker, eliminating the need for local Python environment management. This ensures version control and reproducibility across platforms using Docker and Visual Studio Code.

## Prerequisites

To get started, you’ll need to install the following on your computer:
1. **Docker** – Download and install Docker for your operating system:
   - [Docker for Windows](https://docs.docker.com/desktop/install/windows-install/)
   - [Docker for macOS](https://docs.docker.com/desktop/install/mac-install/)
   - [Docker for Linux](https://docs.docker.com/desktop/install/linux-install/)
2. **Visual Studio Code (VS Code)** – Download and install [VS Code](https://code.visualstudio.com/).
3. **Git** – Git is often pre-installed on Linux, but you may need to install it on Windows and macOS.
   - [Git Installation Guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

   > Note: You’ll also need the **Dev Containers** extension in VS Code, which we’ll cover in the installation steps.

## Step-by-Step Installation Guide

Follow these steps to set up this template on any system:

### Step 1: Clone the Repository

1. Open a terminal on your computer.
2. Run the following command to clone this template from GitHub:
   ```bash
   git clone https://github.com/donphi/data-science-template.git
   ```
3. Navigate to the newly cloned folder:
   ```bash
   cd data-science-template
   ```

### Step 2: Open the Folder in Visual Studio Code

1. Launch **Visual Studio Code**.
2. Click on **File > Open Folder** and select the root folder of the project (`data-science-template`).
3. Once opened, you should see a prompt at the bottom of VS Code asking if you want to "Reopen in Container." Click **Reopen in Container**.

   > **Note**: If you don’t see this prompt, ensure the **Dev Containers** extension is installed in VS Code.

### Step 3: Verify the Dev Container is Running

Once VS Code loads the container:
- Confirm that all project folders (e.g., `data`, `models`, `notebooks`) are visible in the left sidebar.
- Check the bottom-left corner of VS Code for a green icon indicating the container is active.

### Step 4: Working and Saving Changes

- You’re now ready to work within the container! Any code changes or new files will be saved directly in your project directory.
- When you’re ready to update your work on GitHub, use the following commands to commit and push changes:
  ```bash
  git add .
  git commit -m "Describe your changes here"
  git push
  ```

   > **Important**: The `data` folder is ignored by default (based on `.gitignore`) to prevent large or sensitive files from being tracked in Git.

## Alternative Setup (Without Visual Studio Code)

If you’re not using Visual Studio Code, you can still use the `Dockerfile` and `requirements.txt` to set up the environment directly with Docker.

1. **Build the Docker Image**:
   ```bash
   docker build -t your_project_name -f docker/Dockerfile .
   ```
2. **Run the Docker Container**:
   ```bash
   docker run --rm -it --env-file docker/.env -v $(pwd):/workspace your_project_name
   ```
   - The `--env-file` option loads environment variables from `.env`.
   - The `-v $(pwd):/workspace` option mounts your project directory to `/workspace` inside the container.

This setup gives you a similar environment to the Dev Container in VS Code.

---

## Docker and Devcontainer Setup for Environment Consistency

This template uses Docker and VS Code’s Dev Container configuration to ensure consistency and avoid conflicts between local dependencies on different systems.

### Setup Instructions (If Using Docker Directly)

1. **Build the Docker Image**  
   Run the following command to build the Docker image from the `Dockerfile` in the `docker` folder:
   ```bash
   docker build -t your_project_name -f docker/Dockerfile .
   ```

2. **Run the Docker Container**  
   Start a container with the following command:
   ```bash
   docker run --rm -it --env-file docker/.env -v $(pwd):/workspace your_project_name
   ```

3. **Environment Variables**  
   If you don’t want to use the `.env.example` file, you can skip the `.env` setup entirely for Docker. In this case, environment variables can be defined directly in the `docker run` command, like this:
   ```bash
   docker run --rm -it -e VARIABLE_NAME=value -v $(pwd):/workspace your_project_name
   ```
   - Replace `VARIABLE_NAME` and `value` with each environment variable and its value.
   - This method is helpful for quickly setting variables without needing a separate `.env` file but may not be ideal for more complex configurations.
   - If you don’t need certain variables, you can omit `-e VARIABLE_NAME=value` entirely from the command.

4. **Copying `.env.example` for Project-Specific Configurations**  
   Copy `.env.example` to `.env` and update variables as needed:
   ```bash
   cp docker/.env.example docker/.env  # For Linux/macOS
   copy docker\.env.example docker\.env  # For Windows
   ```

### Managing Package Dependencies

- **Add Dependencies**: Add any required dependencies to `docker/requirements.txt`.
- **Install Dependencies in Docker**: When building the Docker image, all dependencies from `requirements.txt` will be installed automatically.

## Project Organization

```
├── .devcontainer               <- Devcontainer files for VS Code Docker setup.
│   └── devcontainer.json       <- VS Code configuration for dev container support.
│
├── docker                      <- Docker-specific files, including Dockerfile and environment files.
│   ├── Dockerfile              <- Dockerfile defining the project environment.
│   ├── .env.example            <- Template for environment variables, to be copied to `.env`.
│   └── requirements.txt        <- List of dependencies for the Docker environment.
│
├── README.md                   <- The top-level README for developers using this project
│
├── data
│   ├── external                <- Data from third party sources
│   ├── interim                 <- Intermediate data that has been transformed
│   ├── processed               <- The final, canonical data sets for modeling
│   └── raw                     <- The original, immutable data dump
│
├── models                      <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks                   <- Jupyter notebooks. Naming convention is a number (for ordering),
│                                  the creator's initials, and a short `-` delimited description, e.g.
│                                  `1.0-jqp-initial-data-exploration`
│
├── references                  <- Data dictionaries, manuals, and all other explanatory materials
│
├── reports                     <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures                 <- Generated graphics and figures to be used in reporting
│
└── src                         <- Source code for this project
    │
    ├── __init__.py             <- Makes src a Python module
    │
    ├── config.py               <- Store useful variables and configuration
    │
    ├── dataset.py              <- Scripts to download or generate data
    │
    ├── features.py             <- Code to create features for modeling
    │
    ├── modeling                <- Code for training and inference
    │   ├── __init__.py 
    │   ├── predict.py          <- Code to run model inference with trained models          
    │   └── train.py            <- Code to train models
    │
    ├── plots.py                <- Code to create visualizations 
    │
    └── services                <- Service classes to connect with external platforms, tools, or APIs
        └── __init__.py 
```

---

*Designed by chonkie*