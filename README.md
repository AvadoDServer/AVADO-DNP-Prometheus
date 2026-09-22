# AVADO-DNP-Prometheus

[Prometheus](https://prometheus.io) package for AVADO. It is installed automatically with the
[Grafana package](https://github.com/AvadoDServer/AVADO-DNP-Grafana).

- UI: http://prometheus.my.ava.do:9090 (targets: http://prometheus.my.ava.do:9090/targets).
  No ports are published on the host; the UI is only reachable from the AVADO network.
- Scrape configuration: [build/prometheus.yml](build/prometheus.yml). It scrapes the
  [node exporter](https://github.com/AvadoDServer/AVADO-DNP-Node-exporter) and the metrics
  endpoints of the Ethereum clients that can be installed on an AVADO (Prysm, Teku, Nimbus,
  Lighthouse, Geth, Nethermind, Erigon, Obol Charon, SSV). Every target is labelled with
  `client` and `network`. Clients that are not installed show up as `down`.

## Retention

Data is kept for `RETENTION_DAYS` days (default `30`) or until it uses `RETENTION_SIZE`
(default `10GB`), whichever comes first. Change both in the package's environment variables
in the AVADO admin UI.

## Upgrading from 0.0.1

0.0.1 ran the untagged `prom/prometheus` image (Prometheus 2.x). 0.0.2 pins Prometheus
v3.14.0, which opens the existing 2.x data directory as is (the TSDB format is unchanged
between 2.x and 3.x). Going back to 2.x afterwards requires Prometheus 2.55 or newer.
