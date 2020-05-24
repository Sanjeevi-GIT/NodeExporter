Stop the running Prometheus process that we left running in the previous lecture, and copy the new files to bin folder.

```cp -r . /usr/local/bin/prometheus```

Create a file called prometheus.service

```sudo nano /etc/systemd/system/prometheus.service```


Add the script and save

```
[Unit]
Description=Prometheus Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/prometheus/prometheus --config.file=/usr/local/bin/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```
Now start and check the service is running.

```
sudo service prometheus start
sudo service prometheus status
```

We can now leave the new Prometheus service running. If you ever need to stop the new Prometheus service, then type

```
sudo service prometheus stop
sudo service prometheus status
```