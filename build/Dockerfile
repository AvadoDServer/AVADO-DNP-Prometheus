FROM --platform=linux/amd64 prom/prometheus

COPY prometheus.yml /etc/prometheus/prometheus.yml
RUN mkdir -p /prometheus/external_configs
COPY charon.yml /prometheus/external_configs