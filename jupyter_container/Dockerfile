# Use Ubuntu as base image
FROM ubuntu:latest

# Install necessary packages
RUN apt-get update && \
    apt-get install -y python3 python3-pip git && \
    pip3 install jupyterlab

# Set working directory and create a user
WORKDIR /home
RUN useradd -m ben

# Switch to user ben
USER ben

# Clone the repository
RUN git clone git@github.com:bthek1/FastAISetup.git

# Expose JupyterLab port
EXPOSE 8888

# Command to start JupyterLab
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser"]