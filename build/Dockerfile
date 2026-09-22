FROM --platform=linux/amd64 prom/prometheus:v3.14.0

COPY prometheus.yml /etc/prometheus/prometheus.yml

# Retention can be changed with the RETENTION_DAYS and RETENTION_SIZE
# environment variables (see dappnode_package.json). Whichever limit is hit
# first wins.
ENV RETENTION_DAYS=30 \
    RETENTION_SIZE=10GB

ENTRYPOINT ["/bin/sh", "-c", "exec /bin/prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/prometheus --storage.tsdb.retention.time=${RETENTION_DAYS:-30}d --storage.tsdb.retention.size=${RETENTION_SIZE:-10GB} --web.enable-lifecycle \"$@\"", "prometheus"]
CMD []
