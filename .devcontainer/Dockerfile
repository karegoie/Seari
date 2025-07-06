# Base image for Julia
FROM julia:1.9-alphine

# Install required dependencies
RUN apt-get update && apt-get install -y \
    git \
    wget \
    unzip \
    build-essential \
    vim \
    && rm -rf /var/lib/apt/lists/*

# Set up environment
ENV JULIA_DEPOT_PATH=/root/.julia
ENV JULIA_PROJECT=@.

# Create a non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && rm -rf /var/lib/apt/lists/*

# Switch to the non-root user
USER $USERNAME

# Set the working directory
WORKDIR /workspaces
