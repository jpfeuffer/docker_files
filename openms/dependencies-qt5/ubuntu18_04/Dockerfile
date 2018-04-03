# Base Image
FROM ubuntu:18.04

# Metadata
LABEL base.image="openms_dependencies:qt5"
LABEL version="1.1"
LABEL software="OpenMS (dependencies)"
LABEL software.version="devel"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"

# Maintainer
MAINTAINER Julianus Pfeuffer
USER root

# Install Step 1: basic dependencies
RUN sudo apt-get -y update && \
         apt-get install -y --no-install-recommends --no-install-suggests g++ autoconf patch libtool cmake make git automake && \
         apt-get install -y --no-install-recommends --no-install-suggests software-properties-common python-software-properties && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Step 4: Qt5
RUN sudo apt-get -y update && \
         apt-get install -y qtbase5-dev && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Step 5: Compiled dependencies
RUN git clone --branch update/zlib1_2_11 https://github.com/jpfeuffer/contrib.git && rm -rf contrib/.git/
RUN mkdir contrib-build

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=ALL ../contrib && rm -rf archives src

WORKDIR /
