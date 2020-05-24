Now that we have at least 3 scrape targets, we can begin to run some more interesting queries that involve multiple scrape targets.

`scrape_duration_seconds`

This shows 3 time series results. 1 for each target,

we can filter for 1 target by including either the instance, or job labels

`scrape_duration_seconds{instance="localhost:9100"}`

Regular Expressions
We can also use regular expressions. Go back to the console view and query for node_cpu_seconds_total We should get about 8 time series results. Lets filter for everything with mode containing irq

`node_cpu_seconds_total{mode=~".*irq"}`

All regular expressions in Prometheus use the [re2](https://github.com/google/re2/wiki/Syntax) syntax.

Data Types
Instant vector
A set of time series containing a single sample for each time series, all sharing the same timestamp `scrape_duration_seconds{instance="localhost:9100"}`

Range Vector
A set of time series containing a range of data points over time for each time series.

Return a whole range of scrape_duration_seconds (in this case 5 minutes) for the same vector, making it a range vector.

`node_netstat_Tcp_InSegs{instance="localhost:9100"}[5m] node_netstat_Tcp_InSegs{instance="localhost:9100"}[1m]` `node_netstat_Tcp_InSegs{instance="localhost:9100"}[30s]`

Press the graph, we get an error saying that expression type "range vector" for range query, must be Scalar or instant Vector

So when in the graph view, remove the [5m] range option.

Functions
`rate(scrape_duration_seconds{instance="localhost:9100"}[1m:20s])`

Start with `node_netstat_Tcp_InSegs`

create a range vector covering 1m `node_netstat_Tcp_InSegs[10m]`

filter for the job prometheus `node_netstat_Tcp_InSegs{job="prometheus"}[10m]`

calculates the per-second average rate of increase of the time series in the range vector `rate(node_netstat_Tcp_InSegs[10m])`

sum the 2 values `sum(go_threads)`

Sub Queries
Start with this instant vector `node_netstat_Tcp_InSegs`

Convert ot to a Range Vecorer and then convert it back to an instant vector using rate rate(node_netstat_Tcp_InSegs[1m])

Wrap it in the ceikling funtion `ceil(rate(node_netstat_Tcp_InSegs[1m]))`

Convert it to a range vecort and get the per-second derivative of the time series `deriv(ceil(rate(node_netstat_Tcp_InSegs[1m]))[1m:])`

https://prometheus.io/docs/prometheus/latest/querying/functions/

https://github.com/prometheus/prometheus/wiki/Default-port-allocations