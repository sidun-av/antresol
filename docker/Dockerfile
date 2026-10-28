# Lumen Server image from the released binaries (no source build).
FROM debian:trixie-slim
ARG TARGETARCH
RUN apt-get update \
 && apt-get install -y --no-install-recommends ffmpeg ca-certificates tzdata curl \
 && rm -rf /var/lib/apt/lists/* \
 && groupadd -g 1000 lumen \
 && useradd -u 1000 -g lumen -G video -m -d /home/lumen -s /usr/sbin/nologin lumen \
 && mkdir -p /config /media && chown lumen:lumen /config /media
COPY bin/${TARGETARCH}/lumen-server /usr/local/bin/lumen-server
COPY LICENSE THIRD_PARTY_LICENSES.md /usr/share/doc/lumen/
ENV VAULT_DATA_DIR=/config VAULT_MEDIA_ROOT=/media
USER lumen
VOLUME /config
EXPOSE 8420
HEALTHCHECK --interval=30s --timeout=5s --start-period=20s --retries=3 \
  CMD curl -fsS http://127.0.0.1:8420/api/health || exit 1
ENTRYPOINT ["/usr/local/bin/lumen-server"]
