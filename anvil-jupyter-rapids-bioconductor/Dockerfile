FROM us.gcr.io/broad-dsp-gcr-public/terra-jupyter-bioconductor:2.1.8

USER root

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 \
    && add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran40/' \
    && echo "deb http://us.archive.ubuntu.com/ubuntu/ bionic universe" >> /etc/apt/sources.list \
    && echo "deb http://security.ubuntu.com/ubuntu/ bionic main" >> /etc/apt/sources.list \
    && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - \
    && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - \
    && apt-get --allow-unauthenticated update && DEBIAN_FRONTEND=noninteractive apt-get install --allow-unauthenticated -y --no-install-recommends \
    git python3-setuptools build-essential libcurl4-gnutls-dev \
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


