FROM debian:bookworm-slim

# Install only what we need:
# - util-linux: nsenter
# - lvm2: pvcreate/vgcreate/pvs/vgs
# - ca-certificates: generally useful in clusters (optional but harmless)
# - coreutils: common basic utils (often already present, but keep it explicit)
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      bash \
      util-linux \
      lvm2 \
      ca-certificates \
      coreutils \
 && rm -rf /var/lib/apt/lists/*

# Keep the image generic; the DaemonSet provides the command/script.
ENTRYPOINT ["/bin/sh", "-c"]
CMD ["sleep infinity"]
