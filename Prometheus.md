# Prometheus

Reference: https://prometheus.io/download/

* move to /opt directory
```
wget https://github.com/prometheus/prometheus/releases/download/v3.0.1/prometheus-3.0.1.linux-amd64.tar.gz
```

* Extract tar file
```
tar -xf prometheus-3.0.1.linux-amd64.tar.gz
```

* Rename if required

```
mv prometheus-3.0.1.linux-amd64 prometheus
```

* Create systemctl service
```
vim /etc/systemd/system/prometheus.service
```

* Enter below info
```
[Unit]
Description=Prometheus Server

[Service]
ExecStart=/opt/prometheus/prometheus --config.file=/opt/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```

```
systemctl start prometheus
```
```
systemctl enable prometheus
```
vi prometheus.yml

# my global config
```
global:
  scrape_interval: 15s
  evaluation_interval: 15s

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets: []

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:

# Scrape configurations
scrape_configs:

  - job_name: "prometheus"

    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "node-1"

    static_configs:
      - targets: ["172.31.13.167:9100"]
```

```
systemctl restart prometheus

```
```
systemctl status prometheus
```

access to prometheus.

```
http://public IP:9090
```

--------------Node-Exporter--------------------------------
* move to /opt directory
```
wget https://github.com/prometheus/prometheus/releases/download/v3.0.1/prometheus-3.0.1.linux-amd64.tar.gz   # download node_exporter as per above starting link.
```

* Extract tar file
```
tar -xf node_expoeter-3.0.1.linux-amd64.tar.gz   # give correct node_exporter tar file.
```

* Rename if required

```
mv prometheus-3.0.1.linux-amd64 node_exporter  # make sure give untar node_exporter file.
```

* Create systemctl service
```
vim /etc/systemd/system/node_exporter.service

# add this content.

[Unit]
Description=Node Exporter

[Service]
ExecStart=/opt/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target

```

```
systemctl restart node_exporter
```

```
systemctl status node_exporter
```


