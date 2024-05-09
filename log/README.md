# Logging

### Running ELK within Docker

Create a configuration file `udp.conf` for Logstash.

```
input {
  udp {
    id => "nodejs_udp_logs"
    port => 7777
    codec => json
  }
}
output {
  elasticsearch {
    hosts => ["localhost:9200"]
    document_type => "nodelog"
    manage_template => false
    index => "nodejs-%{+YYYY.MM.dd}"
  }
}
```

Download Logstash from Dockerhub and configure the service.

```bash
docker run -p 5601:5601 -p 9200:9200 \
  -p 5044:5044 -p 7777:7777/udp \
  -v $PWD/udp.conf:/etc/logstash/conf.d/99-input-udp.conf \
  -e MAX_MAP_COUNT=262144 \
  -it --name distnode-elk sebp/elk:683
```

Visit http://localhost:5601 in your browser. You should see a successful message and verify the service is ready to receive messages.
