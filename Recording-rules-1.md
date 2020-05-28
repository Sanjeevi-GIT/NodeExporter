Time series queries can quickly become quite complicated to remember and type using the Expression Browser in the default Prometheus User Interface.

Example query

```100 - (100 * node_memory_MemFree_bytes / node_memory_MemTotal_bytes)```