# %ARG DOCKER_IMAGE_PARENT
FROM $DOCKER_IMAGE_PARENT
MAINTAINER Gregory Mierzwinski <gmierzwinski@mozilla.com>

# run-task expects to run as root
USER root

RUN apt-get update -qq && \
    apt-get install -y \
      ffmpeg \
      imagemagick \
      pyssim \
      python \
      python-pil \
      python3 \
      python3-pip

WORKDIR /builds/worker

USER worker:worker

COPY requirements.txt /builds/worker/requirements.txt
RUN pip3 install setuptools==46.0.0
RUN pip3 install --require-hashes -r /builds/worker/requirements.txt && \
    rm /builds/worker/requirements.txt

COPY run-visual-metrics.py /builds/worker/bin/run-visual-metrics.py
COPY performance-artifact-schema.json /builds/worker/performance-artifact-schema.json

USER root
RUN chmod +x /builds/worker/bin/run-visual-metrics.py

VOLUME /builds/worker/artifacts/
