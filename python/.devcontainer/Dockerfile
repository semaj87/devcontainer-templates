# Change the tag below to match the Python version required
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
    jq \
    curl \
    wget \
    git \
    zsh \
    && apt-get clean

# Install Neovim via AppImage (uses HTTPS, benefits from Zscaler cert)
RUN curl -L https://github.com/neovim/neovim/releases/latest/download/nvim-linux-arm64.appimage \
    -o /tmp/nvim.appimage \
    && chmod +x /tmp/nvim.appimage \
    && /tmp/nvim.appimage --appimage-extract \
    && mv squashfs-root /opt/nvim \
    && ln -s /opt/nvim/usr/bin/nvim /usr/local/bin/nvim \
    && rm /tmp/nvim.appimage

# Python tools
RUN pip install yq

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
