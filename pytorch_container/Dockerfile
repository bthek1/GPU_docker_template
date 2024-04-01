# Base image with PyTorch and GPU support
FROM pytorch/pytorch:latest

# Install additional packages
RUN apt-get update && \
    apt-get install -y sudo software-properties-common

RUN add-apt-repository -y ppa:bashtop-monitor/bashtop && \
    add-apt-repository -y ppa:flexiondotorg/nvtop && \
    apt-get update

RUN apt-get install -y bashtop nvtop python3-pip \
    vim poppler-utils git openssh-client && \
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
RUN pip install jupyterlab fastai fastbook timm pdf2image pandas

RUN pip install nbdev nbdevAuto

RUN git config --global user.email bthekkel1@gmail.com \
    && git config --global user.name "main_docker"

# COPY /home/ben/'.jupyter' '.jupyter'
ADD /apputils-extension /home/ben/.jupyter/lab/user-settings/@jupyterlab/apputils-extension

# Copy the SSH key into the container
COPY id_ed25519 /home/ben/.ssh/id_ed25519

# Set appropriate permissions on the SSH key and known_hosts
RUN chmod 600 /home/ben/.ssh/id_ed25519 && \
    chown ben:ben /home/ben/.ssh/id_ed25519 && \
    touch /home/ben/.ssh/known_hosts && \
    chmod 644 /home/ben/.ssh/known_hosts && \
    chown ben:ben /home/ben/.ssh/known_hosts

# Add GitHub to known hosts and start SSH agent
RUN ssh-keyscan github.com >> /home/ben/.ssh/known_hosts && \
    eval $(ssh-agent -s)

# Expose Jupyter notebook port
EXPOSE 8888

# Command to start JupyterLab with dark theme
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.theme='JupyterLab Dark'", "--NotebookApp.token='test'"]
