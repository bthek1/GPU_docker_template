# Base image with PyTorch and GPU support
FROM pytorch/pytorch:latest

# Install additional packages
RUN apt-get update && \
    apt-get install -y sudo software-properties-common

RUN add-apt-repository -y ppa:bashtop-monitor/bashtop && \
    add-apt-repository -y ppa:flexiondotorg/nvtop && \
    apt-get update

RUN apt-get install -y bashtop nvtop python3-pip vim poppler-utils git && \
    apt-get clean

# Add /home/ben/.local/bin to the PATH
ENV PATH="/home/ben/.local/bin:${PATH}"

# Add user 'ben'
RUN useradd -m -s /bin/bash ben && \
    echo "ben ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Set working directory
WORKDIR /home/ben

# Switch to user ben
USER ben

# Install Jupyter Lab
RUN pip install jupyterlab fastai fastbook nbdevAuto timm pdf2image

RUN git config --global user.email bthekkel1@gmail.com \
    && git config --global user.name "main_docker"

# Expose Jupyter notebook port
EXPOSE 8888

# COPY /home/ben/'.jupyter' '.jupyter'
ADD /apputils-extension /home/ben/.jupyter/lab/user-settings/@jupyterlab/apputils-extension


# Command to start JupyterLab with dark theme
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.theme='JupyterLab Dark'", "--NotebookApp.token='test'"]
