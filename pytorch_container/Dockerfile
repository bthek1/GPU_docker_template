# Base image with PyTorch and GPU support
FROM pytorch/pytorch:latest

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

# Install Jupyter Lab
RUN pip install jupyterlab

# Add user 'ben'
RUN useradd -m -s /bin/bash ben && \
    echo "ben ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Set working directory
WORKDIR /home

# Expose Jupyter notebook port
EXPOSE 8888

# Switch to user ben
USER ben



# Command to start JupyterLab with dark theme
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.theme='JupyterLab Dark'"]
