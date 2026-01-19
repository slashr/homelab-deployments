FROM kasmweb/ubuntu-noble-desktop:aarch64-1.18.0-rolling-daily

USER root

# Install browser, xdotool, and GPU-related userspace libs.
RUN set -eux; \
    apt-get update -y; \
    apt-get install -y --no-install-recommends \
      ca-certificates \
      curl \
      gnupg \
      apt-transport-https; \
    mkdir -p /etc/apt/keyrings; \
    curl -fsSL https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg \
      -o /etc/apt/keyrings/brave-browser-archive-keyring.gpg; \
    echo "deb [signed-by=/etc/apt/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main" \
      > /etc/apt/sources.list.d/brave-browser-release.list; \
    apt-get update -y; \
    if ! apt-get install -y --no-install-recommends brave-browser; then \
      apt-get install -y --no-install-recommends chromium-browser; \
    fi; \
    apt-get install -y --no-install-recommends \
      xdotool \
      vainfo \
      mesa-utils \
      mesa-va-drivers \
      libva-drm2 \
      libva-x11-2 \
      libva-wayland2 \
      libgbm1 \
      libegl1 \
      libgl1-mesa-dri \
      libdrm2; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*

USER 1000
