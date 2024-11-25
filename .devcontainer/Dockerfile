FROM mcr.microsoft.com/devcontainers/rust:0-1-bullseye

# Update Rust toolchain to the latest stable version
RUN rustup update stable

# Ensure cargo and rustc are in the PATH
ENV PATH="/root/.cargo/bin:${PATH}"

# Include lld linker to improve build times either by using environment variable
# RUSTFLAGS="-C link-arg=-fuse-ld=lld" or with Cargo's configuration file (i.e see .cargo/config.toml).
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
   && apt-get -y install clang lld \
   && apt-get autoremove -y && apt-get clean -y

# Add .cargo/config.toml for lld linker configuration
RUN mkdir -p /root/.cargo && \
    echo '[target.x86_64-unknown-linux-gnu]\nlinker = "clang"\nrustflags = ["-C", "link-arg=-fuse-ld=lld"]' > /root/.cargo/config.toml

# Add .gitignore file
RUN echo '/target\n**/*.rs.bk\nCargo.lock' > /root/.gitignore
