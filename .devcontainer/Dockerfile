FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000
ENV APP_HOME=/workspace

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \ 
    && apt-get update && export DEBIAN_FRONTEND=noninteractive \
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
    unzip \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

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