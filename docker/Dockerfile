FROM ubuntu:22.04

# Forked from ML102
# - replace urls and difrectories
# - replace commit hash

# install system dependencies
# TODO: move ldap-utils, libnss-ldapd, libpam-ldapd, nscd, nslcd to base image??
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        curl \
        git \
        ldap-utils \
        libnss-ldapd \
        libpam-ldapd \
        less \
        nano \
        nodejs \
        nscd \
        nslcd \
        python-is-python3 \
        python3 \
        python3-pip \
        rsync \
        unzip \
        vim \
        wget \
        zip \
    && rm -rf /var/lib/apt/lists/*

# download the required image files into the container image
RUN wget -nv https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz \
        -O /var/lib/flower_photos.tgz \
    && tar -xzf /var/lib/flower_photos.tgz -C /var/lib \
    && rm -f /var/lib/flower_photos.tgz \
    && chown -R root:root /var/lib/flower_photos \
    && chmod -R o+rX /var/lib/flower_photos \
    && wget -nv https://storage.googleapis.com/mledu-datasets/cats_and_dogs_filtered.zip \
        -O /var/lib/cats_and_dogs_filtered.zip \
    && unzip -q -d /var/lib /var/lib/cats_and_dogs_filtered.zip \
    && rm -f /var/lib/cats_and_dogs_filtered.zip \
    && chown -R root:root /var/lib/cats_and_dogs_filtered \
    && chmod -R o+rX /var/lib/cats_and_dogs_filtered

# copy the repo source (e.g. notebooks) to the container image and install dependencies
ARG MWLR_DS_HASH="3d4d78bd405c7751cba4fb7d04d362e8fb522dac" # BIM 29/10/2024 1:27pm
RUN git clone https://github.com/manaakiwhenua/deepseg_workshop.git /opt/mwlr_ds_workshop \
    && cd /opt/mwlr_ds_workshop \
    && git checkout $MWLR_DS_HASH \
    && pip3 --no-cache-dir install -r requirements.txt \
    && pip3 --no-cache-dir install jupyterlab \
    && rm -rf /opt/mwlr_ds_workshop/.git
