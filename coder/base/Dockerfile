FROM codercom/enterprise-base:ubuntu

# Add uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

USER root

RUN apt update && apt install gpg-agent -y && rm -rf /var/lib/apt/lists/*

USER coder
