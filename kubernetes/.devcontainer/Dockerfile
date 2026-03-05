FROM mcr.microsoft.com/devcontainers/base:ubuntu

# System tools
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    jq \
    neovim \
    unzip \
    python3 \
    python3-pip \
    && apt-get clean

# kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s \
    https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" \
    && chmod +x kubectl \
    && mv kubectl /usr/local/bin/

# Helm
RUN curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# k9s
RUN curl -sS https://webinstall.dev/k9s | bash

# kubectx and kubens
RUN curl -Lo /usr/local/bin/kubectx \
    https://github.com/ahmetb/kubectx/releases/latest/download/kubectx \
    && curl -Lo /usr/local/bin/kubens \
    https://github.com/ahmetb/kubectx/releases/latest/download/kubens \
    && chmod +x /usr/local/bin/kubectx /usr/local/bin/kubens

# stern
RUN curl -Lo /usr/local/bin/stern \
    https://github.com/stern/stern/releases/latest/download/stern_linux_amd64 \
    && chmod +x /usr/local/bin/stern

# AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install \
    && rm -rf aws awscliv2.zip

# awsume
RUN pip3 install awsume --break-system-packages
