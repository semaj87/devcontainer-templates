# Change the tag below to match the Python version in pyproject.toml
# Check: [tool.poetry.dependencies] python = "^3.x"
# e.g. 3.9, 3.10, 3.11, 3.12
FROM mcr.microsoft.com/devcontainers/python:3.12

# Add Zscaler CA certificate
# Get zscaler-ca.crt from 1Password and copy to this directory
# cp zscaler-ca.crt .devcontainer/
COPY zscaler-ca.crt /usr/local/share/ca-certificates/zscaler.crt
RUN update-ca-certificates
RUN cat /etc/ssl/certs/* > /root/ca_bundle.pem
ENV REQUESTS_CA_BUNDLE=/root/ca_bundle.pem
ENV SSL_CERT_FILE=/root/ca_bundle.pem
RUN echo "cacert=/root/ca_bundle.pem" >> $HOME/.curlrc

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
    zsh \
    && apt-get clean

# AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install \
    && rm -rf aws awscliv2.zip

# Install Node.js via binary
RUN curl -L https://nodejs.org/dist/v20.19.0/node-v20.19.0-linux-arm64.tar.xz \
    -o /tmp/node.tar.xz \
    && tar -xf /tmp/node.tar.xz -C /usr/local --strip-components=1 \
    && rm /tmp/node.tar.xz

# Python tools
RUN pip install awsume yq

# Claude Code
RUN npm install -g @anthropic-ai/claude-code

# tfswitch
RUN curl -L https://raw.githubusercontent.com/warrensbox/terraform-switcher/release/install.sh | bash

# Install Powerlevel10k
RUN su - vscode -c 'git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
    ~/.oh-my-zsh/custom/themes/powerlevel10k'

# Install zsh plugins
RUN su - vscode -c 'git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
    ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting && \
    git clone https://github.com/zsh-users/zsh-autosuggestions.git \
    ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions && \
    git clone https://github.com/zsh-users/zsh-completions.git \
    ~/.oh-my-zsh/custom/plugins/zsh-completions && \
    git clone https://github.com/zsh-users/zsh-history-substring-search.git \
    ~/.oh-my-zsh/custom/plugins/zsh-history-substring-search'

# Set zsh as default shell for root and vscode user
RUN chsh -s $(which zsh) && chsh -s $(which zsh) vscode
