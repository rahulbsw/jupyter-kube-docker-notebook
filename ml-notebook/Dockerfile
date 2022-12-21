# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/scipy-notebook
ARG PYTHON_VERSION=3.9
FROM $BASE_CONTAINER

ENV TRANSFORMERS_CACHE=/tmp/.cache
ENV TOKENIZERS_PARALLELISM=true

USER root

RUN apt-get update && apt-get install -y graphviz \
    python3-pydot \
    python3-pygraphviz && \
    apt-get clean && rm -rf /var/lib/apt/lists/*



# Add RUN statements to install packages as the $NB_USER defined in the base images.

# Add a "USER root" statement followed by RUN statements to install system packages using apt-get,
# change file permissions, etc.

# If you do switch to root, always be sure to add a "USER $NB_USER" command at the end of the
# file to ensure the image runs as a unprivileged user by default.

USER ${NB_UID}

# Install Python 3 packages

RUN conda install pytorch torchvision torchaudio cpuonly  -c pytorch  --yes

RUN conda install \
    tensorflow \
    jax \
    jaxlib \
    optax  

RUN conda install \
    transformers \
    datasets\
    nltk \
    pytorch_lightning \
    sentencepiece \
    seqeval \ 
    fuzzywuzzy \
    nbgrader \
    rise  -c conda-forge --yes

RUN pip install -y \
    gradio \
    pycaret[full] \
    pandas-profiling \
    modin[all] \
    psycopg2-binary \
    featurewiz \
    dataprep \
    dtale \ 
    sweetviz \
    autoviz \
    pinotdb \
    pandasql \ 
    python-arango \ 
    mysql-connector-python \ 
    scikit-learn \ 
    xgboost \ 
    composeml \ 
    featuretools[complete] 

WORKDIR "${HOME}"
