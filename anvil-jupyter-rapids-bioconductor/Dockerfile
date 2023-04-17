FROM us.gcr.io/broad-dsp-gcr-public/terra-jupyter-bioconductor:2.1.8

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    git python3-setuptools python3-pip build-essential libcurl4-gnutls-dev \
    zlib1g-dev rsync vim cmake tabix

RUN mkdir -p /tmp/rapids && cd /tmp/rapids && git clone \
    https://github.com/cjnolet/AtacWorks.git atacworks && \
    pip3 install \
    scanpy==1.9.1 wget pytabix dash-daq \
    dash-html-components dash-bootstrap-components dash-core-components && \
    cd atacworks && pip3 install . && cd .. && \
    git clone https://github.com/NVIDIA-Genomics-Research/rapids-single-cell-examples.git rapids-single-cell-examples && \
    cd rapids-single-cell-examples && git checkout master && git pull


