# Use Ubuntu as base image
FROM ubuntu:latest

# Install additional packages
RUN apt-get update && \
    apt-get install -y sudo software-properties-common && \
    apt-get update && \
    apt-get install -y python3-pip && \
    add-apt-repository -y ppa:bashtop-monitor/bashtop && \
    add-apt-repository -y ppa:flexiondotorg/nvtop && \
    apt-get update && \
    apt-get install -y bashtop nvtop && \
    apt-get clean

# Install JupyterLab
RUN pip install jupyterlab


# Add user 'ben'
RUN useradd -ms /bin/bash ben
RUN echo 'ben ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Switch to user 'ben'
USER ben


# Set working directory and create a user
WORKDIR /home

# Expose JupyterLab port
EXPOSE 8888

# Command to start JupyterLab
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser"]