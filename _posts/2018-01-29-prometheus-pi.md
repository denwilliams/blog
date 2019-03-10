---
title: Installing Prometheus on a Raspberry Pi
tags:
  - linux
  - prometheus
  - raspberrypi
---

```bash
sudo useradd --no-create-home --shell /bin/false prometheus
sudo useradd --no-create-home --shell /bin/false node_exporter
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /var/lib/prometheus

cd ~
curl -LO https://github.com/prometheus/prometheus/releases/download/v2.1.0/prometheus-2.1.0.linux-armv7.tar.gz
curl -LO https://github.com/prometheus/node_exporter/releases/download/v0.15.2/node_exporter-0.15.2.linux-armv7.tar.gz

tar xvf prometheus-2.1.0.linux-armv7.tar.gz
sudo cp prometheus-2.1.0.linux-amd64/prometheus /usr/local/bin/
sudo cp prometheus-2.1.0.linux-amd64/promtool /usr/local/bin/
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
sudo cp -r prometheus-2.1.0.linux-amd64/consoles /etc/prometheus
sudo cp -r prometheus-2.1.0.linux-amd64/console_libraries /etc/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus/consoles
sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
sudo touch /etc/prometheus/prometheus.yml
sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml

tar xvf node_exporter-0.15.2.linux-armv7.tar.gz
sudo cp node_exporter-0.15.2.linux-amd64/node_exporter /usr/local/bin
sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter

sudo nano /etc/systemd/system/prometheus.service
```

```yml
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```

```bash
sudo nano /etc/systemd/system/node_exporter.service
```

```yml
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

```bash
sudo nano /etc/prometheus/prometheus.yml
```

```yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "prometheus"
    scrape_interval: 5s
    static_configs:
      - targets: ["localhost:9090"]
  - job_name: "node_exporter"
    scrape_interval: 5s
    static_configs:
      - targets: ["localhost:9100"]
```

```bash
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
sudo systemctl start node_exporter
sudo systemctl enable node_exporter
```

> Help from: https://www.digitalocean.com/community/tutorials/how-to-install-prometheus-on-ubuntu-16-04
