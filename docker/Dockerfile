# Use the latest Python image as the base
FROM python:latest

# Set the working directory in the container
WORKDIR /workspace

# Copy only the requirements file first (helps with Docker layer caching)
COPY requirements.txt /workspace/

# Install the dependencies from requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy all contents into the container (for the initial build only)
COPY . /workspace/

# Start Jupyter Notebook server by default
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root"]