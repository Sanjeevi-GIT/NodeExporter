Time series queries can quickly become quite complicated to remember and type using the Expression Browser in the default Prometheus User Interface.

Example query

`node_memory_MemFree_bytes`

`node_memory_MemFree_bytes / node_memory_MemTotal_bytes`

`100 - (100 * node_memory_MemFree_bytes / node_memory_MemTotal_bytes)`

Rather than remembering and typing this query every time, we can create a recording rule that will run at a chosen interval and make the data available as a time series.


## Recording Rule Example 1
cd into the `/usr/local/bin/prometheus `folder


`cd /usr/local/bin/prometheus`
Create a new file called `prometheus_rules.yml`


`sudo vi prometheus_rules.yml`
Add our test expression as a recording rule


```groups:
     - name: custom_rules
       rules:
         - record: node_memory_MemFree_percent
           expr: 100 - (100 * node_memory_MemFree_bytes / node_memory_MemTotal_bytes)


