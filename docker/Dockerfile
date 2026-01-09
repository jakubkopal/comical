# GPU-ready base (CUDA 11.8 + PyTorch). Matches your comical_env.yml intent.
FROM pytorch/pytorch:2.1.0-cuda11.8-cudnn8-runtime

# System deps
RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY . /app

# Upgrade pip and install dependencies (now that requirements.txt exists)
RUN pip install --no-cache-dir -U pip \
 && pip install --no-cache-dir -r requirements.txt
RUN python -m pip install --no-cache-dir --force-reinstall "numpy==1.24.3"

# Quick self-tests
RUN python -c "import sys; print(sys.version)"
RUN python -c "import numpy as np; print('numpy', np.__version__)"
RUN python -c "import torch; print('torch', torch.__version__, 'cuda?', torch.cuda.is_available())"

# Default command (you can change this later)
CMD ["python", "/app/wrapper.py", "--help"]
