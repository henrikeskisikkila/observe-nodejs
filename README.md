# Observe Node.js

This project is dedicated to observing Node.js services that run on remote machines.

## Logging

Logging with the ELK stack, is a reference to Elasticsearch, Logstash, and Kibana.

- Elasticsearch is a database with a powerful query syntax. It exposes an HTTP API.
- Logstash is a service ingesting and transforming logs from multiple sources. You'll create an interface for ingesting log via UPD.
- Kibana is a web service for building dashboards that visualize data stored in Elasticsearch. It exposes an HTTP web service.

### The logging flow

Node.js --> Logstash --> Elasticsearch --> Kibana --> Admin

## Metrics

Metrics help to spot trends of negative performance like slow request handling.

- Graphite
- StatsD
- Grafana

## Alerting

Cabot is an open source tool for polling the health of node services and triggering alerts.
