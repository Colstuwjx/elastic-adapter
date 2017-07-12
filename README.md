# Remote storage adapter

This is a write adapter that receives samples via Prometheus's remote write
protocol and stores them in Elasticsearch.
It is meant as a replacement for the built-in specific remote storage implementations
that have been removed from Prometheus.

## Building

```
go build
```

## Running

Elasticsearch example:

```
./elastic-adapter -elasticsearch-url=http://localhost:9200/ -elasticsearch.max-retries=1 -elasticsearch.index-perfix=prometheus -elasticsearch.type=prom-metric
```

To show all flags:

```
./remote_storage_adapter -h
```

## Configuring Prometheus

To configure Prometheus to send samples to this binary, add the following to your `prometheus.yml`:

```yaml
# Remote write configuration (for Graphite, OpenTSDB, or InfluxDB).
remote_write:
  - url: "http://localhost:9201/write"

# Remote read configuration (for InfluxDB only at the moment).
remote_read:
  - url: "http://localhost:9201/read"
```
