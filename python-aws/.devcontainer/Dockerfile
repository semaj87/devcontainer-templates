# Change the tag below to match the Python version required by the repo
# e.g. 3.9, 3.10, 3.11, 3.12
FROM mcr.microsoft.com/devcontainers/python:3.12

# System tools
RUN apt-get update && apt-get install -y \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    libffi-dev \
    liblzma-dev \
    jq \
    curl \
    wget \
    git \
    && apt-get clean

# Python tools
RUN pip install awsume yq

# Claude Code
RUN npm install -g @anthropic-ai/claude-code
