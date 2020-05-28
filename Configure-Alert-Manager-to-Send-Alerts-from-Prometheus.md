
Edit Alert Manager Configuration
Open the Alert Manager config file, and replace the config with this below.

```
sudo vi /usr/local/bin/alertmanager/alertmanager.yml
```
copy paste below line on to alertmanager.yml

https://github.com/DeekshithSN/Prometheus/blob/master/alertmeanager.yml

Check your configuration with the supplied amtool

```
/usr/local/bin/alertmanager/amtool check-config /usr/local/bin/alertmanager/alertmanager.yml
```
If all is ok, restart the Alert Manager service.

```
sudo service alertmanager restart
sudo service alertmanager status
```
Edit Prometheus Configuration
Open the prometheus.yml configuration file and add the text below to the alerting section

```
sudo vi /usr/local/bin/prometheus/prometheus.yml

```
Add - localhost:9093 to your Alertmanager configuration section

```
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      # alertmanager:9093
      - localhost:9093

```
Check the prometheus configuration with the supplied promtool.

```
/usr/local/bin/prometheus/promtool check config /usr/local/bin/prometheus/prometheus.yml
```
```
sudo service prometheus restart
sudo service prometheus status
```
Test Settings
Check the Prometheus UI

[Status]-->[Runtime and Build Information]

Copy the url in the Alertmanagers section
```
http://localhost:9093/api/v1/alerts
```

Test it using curl
```
curl http://localhost:9093/api/v1/alerts
```
The response should be success.

Now Check the Alert Manager UI

and a new scrape target to the prometheus.yml configuration

```
  - job_name: 'alert-manager'
    static_configs:
    - targets: ['localhost:9093']
```
And restart
```
sudo service prometheus restart
sudo service prometheus status
```