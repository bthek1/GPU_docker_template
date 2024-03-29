# Use Ubuntu as base image
FROM ubuntu:latest

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip3 install jupyterlab && \
    useradd -ms /bin/bash ben

# Switch to the newly created user
USER ben

# Set working directory
WORKDIR /home

# Expose Jupyter Lab port
EXPOSE 8888

# Command to start Jupyter Lab
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
