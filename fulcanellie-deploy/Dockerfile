# Solana CLI requires GLIBC 2.32+ (bullseye has 2.31). Use bookworm.
FROM debian:bookworm-slim

# Set non-interactive frontend for apt
ENV DEBIAN_FRONTEND=noninteractive

# Install required dependencies and Rust
RUN apt-get update && apt-get install -y \
    curl build-essential libssl-dev pkg-config nano \
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Add Rust to PATH
ENV PATH="/root/.cargo/bin:$PATH"

# Verify Rust installation
RUN rustc --version

# Install Solana CLI (non-interactive, no .bashrc)
RUN curl -sSfL https://release.anza.xyz/stable/install | sh -s -- -y

# Add Solana binaries to PATH
ENV PATH="/root/.local/share/solana/install/active_release/bin:${PATH}"

# Verify Solana CLI installation
RUN solana --version

# Set up Solana config for Devnet
RUN solana config set -ud

# Set working directory
WORKDIR /solana-token

# Default command to run a shell
CMD ["/bin/bash"]

