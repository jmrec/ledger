FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

ARG USERNAME=vscode
ENV APP_HOME=/workspace

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    build-essential \
    sudo \
    screen \
    git \
    vim \
    tree \
    postgresql-client \
    ca-certificates \
    curl \
    gnupg \
    unzip

RUN mkdir -p $APP_HOME /home/$USERNAME/.vscode-server/extensions /home/$USERNAME/.vscode-server/data \
    && chown -R $USERNAME:$USERNAME $APP_HOME /home/$USERNAME

WORKDIR $APP_HOME

USER $USERNAME

RUN BIN="/home/vscode/.local/bin" && \
    mkdir -p $BIN && \
    VERSION="1.66.0" && \
    curl -sSL \
    "https://github.com/bufbuild/buf/releases/download/v${VERSION}/buf-$(uname -s)-$(uname -m)" \
    -o "${BIN}/buf" && \
    chmod +x "${BIN}/buf"

ENV PATH="/home/vscode/.local/bin:${PATH}"

EXPOSE 8080