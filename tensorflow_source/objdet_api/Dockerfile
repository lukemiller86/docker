FROM tensorflow_src:latest

# Install Object Detection API dependencies
# https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md
RUN apt-get update && apt-get install -y --no-install-recommends \
        protobuf-compiler \
        python-pil \
        python-lxml \
        python-tk \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Clone TF models repo
RUN git clone https://github.com/tensorflow/models /tensorflow/models

# Compile protobuf libraries and add libraries and TFslim to PYTHONPATH
WORKDIR /tensorflow/models/research/
RUN protoc object_detection/protos/*.proto --python_out=.
ENV PYTHONPATH=${PYTHONPATH}:/tensorflow/models/research:/tensorflow/models/research/slim

WORKDIR /root

RUN pip install filterpy

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

RUN ["/bin/bash"]
