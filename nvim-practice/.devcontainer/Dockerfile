FROM mcr.microsoft.com/devcontainers/base:ubuntu

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
    curl \
    wget \
    git \
    jq \
    zsh \
    unzip \
    software-properties-common \
    && apt-get clean

# Install latest Neovim
RUN add-apt-repository ppa:neovim-ppa/unstable -y && \
    apt-get update && \
    apt-get install -y neovim && \
    apt-get clean

# Set zsh as default shell for root and vscode user
RUN chsh -s $(which zsh) && chsh -s $(which zsh) vscode

# Install Powerlevel10k
RUN su - vscode -c 'git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
    ~/.oh-my-zsh/custom/themes/powerlevel10k'

# Install zsh plugins directly
RUN su - vscode -c 'git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
    ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting && \
    git clone https://github.com/zsh-users/zsh-autosuggestions.git \
    ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions && \
    git clone https://github.com/zsh-users/zsh-completions.git \
    ~/.oh-my-zsh/custom/plugins/zsh-completions && \
    git clone https://github.com/zsh-users/zsh-history-substring-search.git \
    ~/.oh-my-zsh/custom/plugins/zsh-history-substring-search'
