# Base image with PyTorch and GPU support
FROM pytorch/pytorch:latest

# Install additional packages
RUN apt-get update && \
    apt-get install -y sudo software-properties-common

RUN add-apt-repository -y ppa:bashtop-monitor/bashtop && \
    add-apt-repository -y ppa:flexiondotorg/nvtop && \
    apt-get update

RUN apt-get install -y bashtop nvtop python3-pip \
    vim poppler-utils git openssh-client autojump && \
    apt-get clean

# Add user 'ben'
RUN useradd -m -s /bin/bash ben && \
    echo "ben ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Set working directory
WORKDIR /home/ben

RUN echo ". /usr/share/autojump/autojump.sh" >> /home/ben/.bashrc

RUN git config --global user.email bthekkel1@gmail.com \
    && git config --global user.name "main_docker"

# COPY /home/ben/'.jupyter' '.jupyter'
COPY /apputils-extension /home/ben/.jupyter/lab/user-settings/@jupyterlab/apputils-extension
COPY .bashrc /home/ben/.bashrc
COPY .bashrc.local /home/ben/.bashrc.local

# Expose Jupyter notebook port
EXPOSE 8888

# Add /home/ben/.local/bin to the PATH
ENV PATH="/home/ben/.local/bin:${PATH}"

# Switch to user ben
USER ben

# Copy requirements file
COPY requirements.txt .

# Install required Python packages
RUN pip install jupyterlab
# Install required Python packages
RUN pip install fastai
# Install required Python packages
RUN pip install fastbook

# Install required Python packages
RUN pip install -r requirements.txt

RUN jupyter notebook password --generate-config && \
    echo "c.NotebookApp.password='3719'" >> /home/ben/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.token = '3719'" >>/home/ben/.jupyter/jupyter_notebook_config.py
    
    
# Command to start JupyterLab with dark theme
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.theme='JupyterLab Dark'", "--NotebookApp.token=''", "--allow-root", "--NotebookApp.password=''"]
