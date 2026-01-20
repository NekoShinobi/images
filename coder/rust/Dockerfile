FROM codercom/enterprise-base:ubuntu

# Add uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/


USER root

ENV RUSTUP_HOME=/opt/rustup
ENV CARGO_HOME=/opt/cargo
ENV PATH=/opt/cargo/bin:$PATH

# Packages needed based on using rust-discord-bot project.
RUN apt update && apt install -y pkg-config cmake libssl-dev gpg-agent && rm -rf /var/lib/apt/lists/*

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --no-modify-path --profile minimal --default-toolchain nightly --default-host x86_64-unknown-linux-gnu && \
    chmod -R a+w ${RUSTUP_HOME} ${CARGO_HOME}

 # TODO: Remove when this issue is fixed: https://github.com/nestybox/sysbox/issues/973 
 # Temporarly fix containerd version 
 RUN set -eux; \ 
     . /etc/os-release; \ 
     if [ -z "${VERSION_ID:-}" ] || [ -z "${VERSION_CODENAME:-}" ]; then \ 
         echo "Unable to detect Ubuntu version metadata"; exit 1; \ 
     fi; \ 
     apt-get update; \ 
     apt-get install -y --allow-downgrades "containerd.io=1.7.28-1~ubuntu.${VERSION_ID}~${VERSION_CODENAME}" && \ 
     apt-mark hold containerd.io 

USER coder
