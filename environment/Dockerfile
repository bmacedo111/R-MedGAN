# hash:sha256:f683d3ef4733b65bc6670e03f7fc45a593b3011ebfc371e53364940d3a48abc5

# Use Miniconda with CUDA support
FROM registry.codeocean.com/codeocean/miniconda3:4.9.2-cuda11.7.0-cudnn8-ubuntu20.04

ARG DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    graphviz \
    libgraphviz-dev \
    pkg-config \
    python3-dev \
    libxrender1 \
    libxext6 \
    && rm -rf /var/lib/apt/lists/*

# Install Jupyter and Python dependencies
RUN pip install -U --no-cache-dir \
    jupyter \
    notebook \
    jupyterlab \
    matplotlib==3.7.1 \
    pandas \
    networkx \
    pygraphviz \
    rdkit==2022.3.5 \
    tensorflow==2.12.0 \
    tqdm==4.66.1 \
    numpy==1.23.5

# Set Jupyter to launch
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]


