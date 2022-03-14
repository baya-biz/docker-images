FROM --platform=$BUILDPLATFORM ubuntu:20.04

ARG TARGETOS TARGETARCH

WORKDIR /workspaces/install

# To workaround rustc's interactive prompts during installation.
ENV DEBIAN_FRONTEND=noninteractive

# Install the required system dependencies.
RUN apt update && \
      apt upgrade && \
      apt install -y \
            build-essential curl git lsb-release gnupg unzip vim

# Install awscli v2.
RUN curl "https://awscli.amazonaws.com/awscli-exe-${TARGETOS}-${TARGETARCH}.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip && \
      ./aws/install && \
      rm -rf ./aws ./awscliv2.zip

# Install NodeJS 14.x, pnpm and rush.
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt install nodejs && \
      npm i -g pnpm && \
      pnpm add -g @microsoft/rush

# Install goreman.
RUN curl "https://github.com/mattn/goreman/releases/download/v0.3.11/goreman_v0.3.11_${TARGETOS}_${TARGETARCH}.tar.gz" -o "goreman.zip"
RUN tar -xvf goreman.tar.gz && \
      mv ./goreman_v0.3.11_${TARGETOS}_${TARGETARCH}/goreman goreman && \
      rm -rf ./goreman.zip ./goreman_v0.3.11_${TARGETOS}_${TARGETARCH}

# Install sops.
RUN curl "https://github.com/mozilla/sops/releases/download/v3.7.2/sops-v3.7.2.${TARGETOS}.${TARGETARCH}" -o "sops"
