Now we will install the Prometheus Node Exporter on our existing server and configure it as a Service so that it keeps running in the background.

We will download the node exporter binary from the Prometheus downloads page at https://prometheus.io/download/#node_exporter

Download Prometheus Node Exporter Binary
SSH into your Prometheus server, and run


```wget https://github.com/prometheus/node_exporter/releases/download/v0.18.1/node_exporter-0.18.1.linux-amd64.tar.gz```

Untar it,

```tar xzf node_exporter-0.18.1.linux-amd64.tar.gz```

Copy it to the /usr/local/bin/ folder

```cp node_exporter-0.18.1.linux-amd64/node_exporter /usr/local/bin/node_exporter```

Configure Prometheus Node Exporter as a Service, Create a file called node-exporter.service

``` sudo vi /etc/systemd/system/node-exporter.service ```

Add the script and save
```
[Unit]
Description=Prometheus Node Exporter Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target

```
Now start and check the service is running.
```
systemctl daemon-reload
sudo service node-exporter start
sudo service node-exporter status
```
Node exporter will now be running on http://[your domain or ip]:9100/metrics


Add the new scrape config for the new node exporter.


sudo vi /usr/local/bin/prometheus/prometheus.yml
Scroll down to the bottom and add a new scrape config

```
  - job_name: 'node-exporter'
    static_configs:
    - targets: ['localhost:9100']
```

and restart the prometheus service.

```
sudo service prometheus restart
sudo service prometheus status
```