What is Prometheus?

Prometheus is a time series database. Prometheus is designed to monitor targets. Servers, databases, standalone virtual machines, pretty much everything can be monitored with Prometheus.


When does it fit?

* Prometheus works well for recording any purely numeric time series
* It fits both machine-centric monitoring and highly dynamic service-oriented architectures.
* Prometheus is designed for reliability, during an system outage it allow you to quickly diagnose problems. 
* Each Prometheus server is standalone, does not depend on any network storage or other remote services.

When does it not fit?

* If you need 100% accuracy, such as for per-request billing, Prometheus is not a good choice

For more information refer :- https://prometheus.io/docs/introduction/overview/
