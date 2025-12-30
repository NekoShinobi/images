FROM codercom/enterprise-base:ubuntu

# Add uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

RUN apt update && apt install gpg-agent && rm -rf /var/lib/apt/lists/*
