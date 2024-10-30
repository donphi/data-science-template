# Data Project Template

## Overview
This project template is based on a simplified version of the [Cookiecutter Data Science](https://cookiecutter-data-science.drivendata.org) template. It is designed to support AI and data science projects using Docker for a reproducible environment setup.

## Adjusting `.gitignore`
Ensure you adjust the `.gitignore` file according to your project needs. For example, in this template, the `/data/` folder is excluded from source control by default.

Typically, you want to exclude this folder if it contains either sensitive data that you do not want to add to version control or large files.

## Docker for Environment Setup
This template uses Docker to create a consistent and isolated environment for your project, avoiding conflicts between local dependencies and ensuring compatibility across different systems.

### Docker Setup
1. **Build the Docker Image**  
   Run the following command to build the Docker image from the Dockerfile in the `docker` folder:
   ```bash
   docker build -t your_project_name -f docker/Dockerfile .
   ```

2. **Run the Docker Container**  
   After building the image, start a container using:
   ```bash
   docker run --rm -it --env-file docker/.env -v $(pwd):/app your_project_name
   ```
   - The `--env-file` option loads environment variables from the `.env` file located in the `docker` folder.
   - The `-v $(pwd):/app` option mounts your project directory to `/app` in the container, allowing changes in your local directory to reflect inside the Docker container.

3. **Environment Variables**
   If you don’t want to use the `.env.example` file, you can skip the `.env` setup entirely for Docker. In this case, environment variables can be defined directly in the `docker run` command, like this:
   ```bash
   docker run --rm -it -e VARIABLE_NAME=value -v $(pwd):/app your_project_name
   ```
   - Replace `VARIABLE_NAME` and `value` with each environment variable and its value.
   - This method is helpful for quickly setting variables without needing a separate `.env` file but may not be ideal for more complex configurations.
   - If you don’t need certain variables, you can omit `-e VARIABLE_NAME=value` entirely from the command.

4. **Copying `.env.example` for Projects Using .env**  
   If you prefer to use a `.env` file, copy the `.env.example` file in the `docker` folder to `.env`, then edit it with your project-specific environment variables. To copy the file:
   ```bash
   cp docker/.env.example docker/.env # Linux, macOS, Git Bash, WSL
   copy docker\.env.example docker\.env # Windows Command Prompt
   ```

### Package Dependencies
The dependencies are managed through a `requirements.txt` file located in the `docker` folder. This file specifies all packages required by your project.

- **Adding Dependencies**: Add any additional dependencies directly to `docker/requirements.txt`.
- **Installing Dependencies in Docker**: When building the Docker image, all dependencies from `requirements.txt` are automatically installed in the container.


## Project Organization

```
├── docker                   <- Docker-specific files, including Dockerfile and environment files.
│   ├── Dockerfile           <- Dockerfile defining the project environment.
│   ├── .env.example         <- Template for environment variables, to be copied to `.env`.
│   └── requirements.txt     <- List of dependencies for the Docker environment.
│
├── README.md                <- The top-level README for developers using this project
│
├── data
│   ├── external             <- Data from third party sources
│   ├── interim              <- Intermediate data that has been transformed
│   ├── processed            <- The final, canonical data sets for modeling
│   └── raw                  <- The original, immutable data dump
│
├── models                   <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks                <- Jupyter notebooks. Naming convention is a number (for ordering),
│                               the creator's initials, and a short `-` delimited description, e.g.
│                               `1.0-jqp-initial-data-exploration`
│
├── references               <- Data dictionaries, manuals, and all other explanatory materials
│
├── reports                  <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures              <- Generated graphics and figures to be used in reporting
│
└── src                      <- Source code for this project
    │
    ├── __init__.py          <- Makes src a Python module
    │
    ├── config.py            <- Store useful variables and configuration
    │
    ├── dataset.py           <- Scripts to download or generate data
    │
    ├── features.py          <- Code to create features for modeling
    │
    ├── modeling             <- Code for training and inference
    │   ├── __init__.py 
    │   ├── predict.py       <- Code to run model inference with trained models          
    │   └── train.py         <- Code to train models
    │
    ├── plots.py             <- Code to create visualizations 
    │
    └── services             <- Service classes to connect with external platforms, tools, or APIs
        └── __init__.py 

```

--------