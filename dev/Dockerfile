FROM ubuntu:20.04

WORKDIR /workspaces/install

# To workaround rustc's interactive prompts during installation.
ENV DEBIAN_FRONTEND=noninteractive

# Add Github CLI registry.
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

RUN apt update && \
      apt upgrade && \
      apt install -y \
            build-essential curl git lsb-release gh gnupg unzip vim

# Install awscli v2.
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip && \
      ./aws/install && \
      rm -rf ./aws ./awscliv2.zip

# Install NodeJS 14.x, pnpm and rush.
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt install nodejs && \
      npm i -g pnpm && \
      pnpm add -g @microsoft/rush
