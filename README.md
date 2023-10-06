# prometheus-workshop

## Resources

- [Prometheus](https://prometheus.io/)
- [What is Prometheus](https://last9.io/blog/what-is-prometheus/)
- [Samples vs Metrics vs Cardinality](https://last9.io/blog/sample-vs-metrics-vs-cardinality/)
- [PromQL Querying](https://prometheus.io/docs/prometheus/latest/querying/basics/)
- [Metric Types](https://last9.io/blog/prometheus-monitoring/#prometheus-metric-types)
- [Prometheus and Grafana](https://last9.io/blog/prometheus-and-grafana/)
- [What is High Cardinality](https://last9.io/blog/what-is-high-cardinality/)

## Pre-requisites

- [Docker setup](https://www.docker.com/get-started/)
- If you don't have Docker setup, try [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/prathamesh-sonpatki/gitpod-starter)

## Milestone 1: Installing Prometheus

``` shell
docker run -p -d 9090:9090 prom/prometheus
```

### Lab

- [ ] Visit `http://localhost:9090`
- [ ] See all the metrics scraped by Prometheus about itself.

## Milestone 2: Tour De Prometheus

### Lab

- [ ] Play around each of the pages and tabs in Prometheus.
- [ ] Go through Prometheus configuration.
- [ ] Go through Targets.


## Milestone 3: First taste of querying

### Lab


- [ ] Run a query to understand if Prometheus is up and running.
- [ ] Run a query to know how many samples are ingested by Prometheus. Hint: `tsdb_head_samples_ap...`

## Milestone 4: Instrumenting an HTTP service

### Updated Prometheus Configuration

``` yaml
global:
  scrape_interval: 15s

scrape_configs:
  # Scrape Prometheus itself
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  # Scrape the service running on localhost:8080
  - job_name: 'api-service'
    static_configs:
      - targets: ['locaohost:8080']
```

### Running Prometheus with updated configuration

``` shell
docker run -d \
  -p 9090:9090 \
  -v $(pwd)/prometheus.yml:/etc/prometheus/prometheus.yml \
  prom/prometheus
```

### Running HTTP Service

``` shell
docker run -d -p 8080:8080 pierrevincent/prom-http-simulator:0.1
```

### Lab

- [ ] **Exercise**: See all metrics exposed by the HTTP service.

## Milestone 5: Monitoring an application

## Milestone 6: Alerting 102

## Milestone 7: See with Grafana

## Milestone 8: Advanced Topics: Relabeling

## Milestone 9: Advanced Topics: Remote Write to Long Term Storage like Levitate
