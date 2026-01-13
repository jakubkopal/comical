FROM nvcr.io/nvidia/pytorch:23.10-py3

ENV PYTHONUNBUFFERED=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PIP_NO_CACHE_DIR=1

RUN apt-get update && apt-get install -y --no-install-recommends \
      git ca-certificates \
      libglib2.0-0 libsm6 libxext6 libxrender1 \
    && rm -rf /var/lib/apt/lists/*

RUN python -m pip install --upgrade pip setuptools wheel
RUN python -m pip install "numpy<2"

COPY requirements.txt /opt/swinbrain/requirements.txt
RUN python -m pip install -r /opt/swinbrain/requirements.txt
RUN python -m pip install --upgrade --force-reinstall "numpy<2"
