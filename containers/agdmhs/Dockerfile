# Set up variables
FROM algorun/algorun:16.04
MAINTAINER Andrew Gainer-Dewar, Ph.D. <andrew.gainer.dewar@gmail.com>

# Add any algorithm dependencies here
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    libboost-log-dev \
    libboost-program-options-dev \
    libboost-system-dev \
    python-dev \
    python-pip \
    git \
    build-essential \
    && rm -rf /var/lib/apt/lists/

RUN git clone https://github.com/simplejson/simplejson \
    && cd simplejson \
    && git checkout v3.11.0 \
    && python setup.py install \
    && cd .. \
    && rm -rf simplejson

# Fetch and build the code
COPY ./src /home/algorithm/src/
WORKDIR /home/algorithm/src/alg
RUN make
WORKDIR /home/algorithm/src

# Add the Algorun manifest and examples
COPY ./algorun_info /home/algorithm/web/algorun_info/

# Add your command to execute an algorithm as environment variable EXEC_COMMAND
ENV EXEC_COMMAND "mhs"
