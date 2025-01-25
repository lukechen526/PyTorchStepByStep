# Use NVIDIA CUDA 12.1 base image with development tools
ARG BASE_IMAGE=nvidia/cuda:12.1.1-devel-ubuntu22.04
FROM ${BASE_IMAGE}

# Install system dependencies
RUN apt-get update && \
    apt-get install -y wget git bzip2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Miniconda
ENV CONDA_DIR /opt/conda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh && \
    bash miniconda.sh -b -p $CONDA_DIR && \
    rm miniconda.sh

# Add Conda to PATH
ENV PATH $CONDA_DIR/bin:$PATH

# Copy environment file
COPY environment.yml /tmp/environment.yml

# Create Conda environment
RUN conda env create -f /tmp/environment.yml

# Set up shell to activate environment
RUN echo "source $CONDA_DIR/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate pytorchbook" >> ~/.bashrc

SHELL ["/bin/bash", "--login", "-c"]

WORKDIR /workspace

CMD ["/bin/bash"]