FROM us.gcr.io/broad-dsp-gcr-public/terra-jupyter-bioconductor:2.1.8

USER root

RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    sudo apt-get install apt-transport-https ca-certificates gnupg && \
    sudo apt-get update && DEBIAN_FRONTEND=noninteractive sudo apt-get install -y --no-install-recommends \
    git python3-setuptools python3-pip build-essential libcurl4-gnutls-dev \
    zlib1g-dev rsync vim cmake tabix

RUN mkdir -p /tmp/rapids && cd /tmp/rapids && git clone \
    https://github.com/cjnolet/AtacWorks.git atacworks && \
    pip3 install \
    scanpy==1.9.1 wget pytabix dash-daq \
    dash-html-components dash-bootstrap-components dash-core-components && \
    cd atacworks && pip3 install . && cd .. && \
    git clone https://github.com/NVIDIA-Genomics-Research/rapids-single-cell-examples.git rapids-single-cell-examples && \
    cd rapids-single-cell-examples && git checkout master && git pull && chown -R jupyter /tmp/rapids

USER jupyter


