ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/scipy-notebook
ARG PYTHON_VERSION=3.9
FROM $BASE_CONTAINER

LABEL maintainer="Rahul Jain"
LABEL name="datascience-notebook"

# Fix: https://github.com/hadolint/hadolint/wiki/DL4006
# Fix: https://github.com/koalaman/shellcheck/wiki/SC3014
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Install all OS dependencies for notebook server that starts but lacks all
# features (e.g., download as all possible file formats)
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y graphviz \
    python3-pydot \
    python3-pygraphviz && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
    
USER ${NB_UID}

WORKDIR "${HOME}"

ENV TRANSFORMERS_CACHE=/tmp/.cache
ENV TOKENIZERS_PARALLELISM=true

COPY environment.yml .
RUN mamba env create -f environment.yml
RUN source activate jupyterenv
RUN echo "source activate jupyterenv" > ${HOME}/.bashrc
