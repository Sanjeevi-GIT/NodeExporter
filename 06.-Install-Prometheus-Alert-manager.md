Download the latest Prometheus Alert Manager binary from 

https://prometheus.io/download/#alertmanager

```
wget https://github.com/prometheus/alertmanager/releases/download/v0.19.0/alertmanager-0.19.0.linux-amd64.tar.gz
```
```
tar xvfz alertmanager-0.19.0.linux-amd64.tar.gz
```
CD into the new alertmanager-0.19.0.linux-amd64 folder

```
cd alertmanager-0.19.0.linux-amd64
ls -ltr
```
Try and run it,

```
./alertmanager --config.file=alertmanager.yml
```
Note that it's running on port 9093

Stop the running process, and copy the new files to bin folder.

```
cp -r . /usr/local/bin/alertmanager
```
Create a file called alertmanager.service

```
sudo vi/etc/systemd/system/alertmanager.service
```
Add the script and save

```
[Unit]
Description=Prometheus Alert Manager Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/alertmanager/alertmanager \
        --config.file=/usr/local/bin/alertmanager/alertmanager.yml 
[Install]
WantedBy=multi-user.target
```
Now start and check the service is running.
```
sudo service alertmanager start
sudo service alertmanager status
```
We can now leave the new Prometheus Alert Manager service running. If you ever need to stop the new Prometheus Alert Manager service, then type

```
sudo service alertmanager stop
sudo service alertmanager status
```
Try http://your_ip_adrress:9093/