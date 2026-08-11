# Tripwire cluster bootstrap image: Node for schema apply + baked-in
# scripts/sandbox so Modal setup does not need blob mounts.
FROM docker.io/library/node:22-bookworm

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    python3 \
    python3-pip \
    python3-venv \
  && rm -rf /var/lib/apt/lists/*

# Modal CLI for non-interactive token auth + secret sync + deploy.
# bookworm's PEP 668 requires --break-system-packages for system pip.
# python-dotenv is required by `modal secret create --from-dotenv`.
RUN pip3 install --no-cache-dir --break-system-packages 'modal>=0.73' 'python-dotenv'

WORKDIR /app

# Repo-layout paths expected by scripts/setup-modal.sh (ROOT=parent of scripts/).
COPY scripts/ /app/scripts/
COPY sandbox/ /app/sandbox/

RUN chmod +x /app/scripts/setup-modal.sh \
  && chmod +x /app/scripts/_modal_env_split.py

CMD ["sleep", "infinity"]
