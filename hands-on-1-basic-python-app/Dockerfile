# This Dockerfile is for a basic Python application.

# Use the official latest version of Ubuntu image as the base image
FROM ubuntu:latest

# set the working directory in the container
WORKDIR /app1

# Copy the current directory contents into the container at /app1
COPY . /app1

# Installs Python 3 and pip inside the container
RUN apt-get update && apt-get install -y python3 python3-pip

# This sets an environment variable NAME with a default value World
ENV NAME World

# This sets the default command that runs when the container starts.
CMD ["python3", "app.py"]