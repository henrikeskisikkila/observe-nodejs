# Metrics

A metric is numeric data associated with time. This can be e.g. request rates, the number of 2XX versus 5XX HTTP responses, latency between the application and a backing service, memory and disk use, and even business stats like dollar revenue or cancelled payments.

- StatsD (A daemon for collecting metrics over TCP or UDP)
- Graphite (Carbon service an time series database Whisper)
- Grafana (A web service that queries time series backends like Graphite and displays information)

Run Graphite

```
docker run \
  -p 8080:80 \
  -p 8125:8125/udp \
  -it --name distnode-graphite graphiteapp/graphite-statsd:1.1.6-1
```

Run Grafana

```
docker run \
  -p 8000:3000 \
  -it --name distnode-grafana grafana/grafana:6.5.2
```

Visit the Grafana dashboard at http://localhost:8000/

Configure Grafana to use Graphite

Set url and version:

```
http://local_ip:8080
Version: 1.1.x
```

```
// Get your localh IP address
ipconfig getifaddr en0.
```

Run each command in a separate terminal window. These commands will generate a stream of data, which gets passed to StatD before being sent to Graphite.

```
NODE_DEBUG=statsd-client node consumer-http-metrics.js
node producer-http-basic.js
autocannon -d 300 -R 5 -c 1 http://localhost:3000
watch -n1 curl http://localhost:3000/error
```
