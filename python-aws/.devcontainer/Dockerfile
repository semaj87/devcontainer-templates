# Change the tag below to match the Python version in pyproject.toml
# Check: [tool.poetry.dependencies] python = "^3.x"
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
    neovim \
    zsh \
    && apt-get clean

# Install Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && apt-get clean

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
