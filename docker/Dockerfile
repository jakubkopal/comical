FROM python:3.11-slim

# System deps commonly needed for scientific python + git-based installs
RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY . /app

# Upgrade pip
RUN pip install --no-cache-dir -U pip

# If the repo has requirements.txt, install it (won't fail if missing)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi

# Install the project itself (editable) if it is a python package
RUN pip install --no-cache-dir -e . || true

# Quick self-test (will run during build logs)
RUN python -c "import sys; print(sys.version)"

CMD ["python", "-c", "print('Container is ready')"]

