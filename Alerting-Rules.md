Alerting rules are created in Prometheus very similar to how you create recording rules. We can use the same prometheus_rules.yml or, if you wish, create a different file but remember to add the reference to it in the rule_files section in prometheus.yml

We will create a new group named alert_rules.

And add the script below.

```
  - name: alert_rules
    rules:
      - alert: InstanceDown
        expr: up == 0
        for: 1m
        labels:
          severity: critical
        annotations:
          summary: "Instance [{{ $labels.instance }}] down"
          description: "[{{ $labels.instance }}] of job [{{ $labels.job }}] has been down for more than 1 minute."
```
Save it and test it with the promtool

```
./promtool check rules prometheus_rules.yml
```
If everything is ok, then restart Prometheus.

```
sudo service prometheus restart
sudo service prometheus status
```
Next we create another rule that uses one of the Recording rules we created in the previous lecture, node_filesystem_free_percent

```
  - alert: DiskSpaceFree10Percent
    expr: node_filesystem_free_percent <= 10
    labels:
      severity: warning
    annotations:
      summary: "Instance [{{ $labels.instance }}] has 10% or less Free disk space"
      description: "[{{ $labels.instance }}] has only {{ $value }}% or less free."
```