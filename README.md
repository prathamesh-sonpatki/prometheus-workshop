# prometheus-workshop

## Resources

- [Prometheus](https://prometheus.io/)
- [What is Prometheus](https://last9.io/blog/what-is-prometheus/)
- [Samples vs Metrics vs Cardinality](https://last9.io/blog/sample-vs-metrics-vs-cardinality/)
- [PromQL Querying](https://prometheus.io/docs/prometheus/latest/querying/basics/)
- [Querying Examples](https://prometheus.io/docs/prometheus/latest/querying/examples/)
- [Metric Types](https://last9.io/blog/prometheus-monitoring/#prometheus-metric-types)
- [Prometheus and Grafana](https://last9.io/blog/prometheus-and-grafana/)
- [What is High Cardinality](https://last9.io/blog/what-is-high-cardinality/)
- [Prometheus: Best Practices and Beastly Pitfalls](https://www.youtube.com/watch?v=_MNYuTNfTb4)
- [Robust Perception Blog](https://www.robustperception.io/blog/)

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

- [ ] See all metrics exposed by the HTTP service.
- [ ] Verify that Prometheus is able to scrape metrics from HTTP service.

## Milestone 5: Monitoring an application

### Lab

- [ ] See all metrics and corresponding labels emitted by the HTTP service.
- [ ] `up{job="api-service"}`
- [ ] Let's look at the number of requests that this service has received since it started up.
- [ ] All requests with status 200 and endpoint `/login`.
- [ ] First taste of aggregation, do a `sum` of all requests with status 200 and endpoint `/login`.
- [ ] How do we get data for a range instead of a single timestamp? Range vector vs. instant vector.
- [ ] Rate of change in the number of requests, use the `rate` function.
- [ ] What's the overall request rate (with a 1 minute rolling-window)
- [ ] How many requests per minute are errors?
- [ ] What's the error rate (in %) of requests to the /users endpoint?
- [ ] Top requested endpoints by status code


## Milestone 6: Alerting 102

## Milestone 7: See with Grafana

``` shell
docker run -d -p 3000:3000 grafana/grafana-oss
```

### Lab

- [ ] First visit to Grafana.
- [ ] Adding a data source.
- [ ] Create a dashboard.
- [ ] Add all previous queries as panels.
- [ ] Graph of latency distribution
- [ ] Cumulative % graph of endpoint request rate
- [ ] Memory usage over time
- [ ] CPU usage over time
- [ ] Graph % of requests fulfilling the SLO of 400ms for /login endpoint


## Milestone 8: Advanced Topics: Relabeling

## Milestone 9: Advanced Topics: Remote Write to Long Term Storage like Levitate
