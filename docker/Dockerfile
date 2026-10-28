# Antresol Server image from the released binaries (no source build).
FROM debian:trixie-slim
ARG TARGETARCH
RUN apt-get update \
 && apt-get install -y --no-install-recommends ffmpeg ca-certificates tzdata curl \
 && rm -rf /var/lib/apt/lists/* \
 && groupadd -g 1000 antresol \
 && useradd -u 1000 -g antresol -G video -m -d /home/antresol -s /usr/sbin/nologin antresol \
 && mkdir -p /config /media && chown antresol:antresol /config /media
COPY bin/${TARGETARCH}/antresol-server /usr/local/bin/antresol-server
COPY LICENSE THIRD_PARTY_LICENSES.md /usr/share/doc/antresol/
ENV VAULT_DATA_DIR=/config VAULT_MEDIA_ROOT=/media
USER antresol
VOLUME /config
EXPOSE 8420
HEALTHCHECK --interval=30s --timeout=5s --start-period=20s --retries=3 \
  CMD curl -fsS http://127.0.0.1:8420/api/health || exit 1
ENTRYPOINT ["/usr/local/bin/antresol-server"]
