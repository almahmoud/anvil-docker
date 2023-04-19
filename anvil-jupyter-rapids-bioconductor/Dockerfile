FROM us.gcr.io/broad-dsp-gcr-public/terra-jupyter-bioconductor:2.1.8

USER root

RUN rm -rf /etc/apt/sources.list.d && rm /etc/apt/sources.list \
    && echo "deb http://security.ubuntu.com/ubuntu/ bionic main" >> /etc/apt/sources.list \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    git python3-setuptools build-essential libcurl4-gnutls-dev \
    zlib1g-dev rsync vim cmake tabix \
    && mkdir -p /tmp/rapids && cd /tmp/rapids && git clone \
    https://github.com/cjnolet/AtacWorks.git atacworks && \
    pip3 install \
    scanpy==1.9.1 wget pytabix dash-daq \
    dash-html-components dash-bootstrap-components dash-core-components && \
    cd atacworks && pip3 install . && cd .. && \
    git clone https://github.com/NVIDIA-Genomics-Research/rapids-single-cell-examples.git rapids-single-cell-examples && \
    cd rapids-single-cell-examples && git checkout master && git pull && chown -R jupyter /tmp/rapids && chown -R jupyter /home/jupyter

USER jupyter

RUN cd /tmp/rapids/rapids-single-cell-examples && /opt/conda/bin/conda env create --name rapidgenomics -f conda/rapidgenomics_cuda11.5.yml && /opt/conda/bin/conda init && source ~/.bashrc && conda activate rapidgenomics && python -m ipykernel install --user --display-name "Python (rapidgenomics)"

