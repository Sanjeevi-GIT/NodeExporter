We will install the latest version of Prometheus on our server.

Before you start, you will need a Linux server. Preferably an unrestricted Ubuntu 16.04 LTS Server with root access, since all the commands demonstrated in this are executed on Ubuntu 16.04 LTS Server.

You can use other operating systems, such as Centos 7, but all commands in the course are prepared for Ubuntu 18, so you will experience some differences in syntax or equivalent commands which you may need to research yourself if I can't help you.

Once you have an Ubuntu 18 server ready, you can find the latest version of the Prometheus binary to download at https://prometheus.io/download/

Or just copy/paste this pre created command below for prometheus-2.14.

```wget https://github.com/prometheus/prometheus/releases/download/v2.18.1/prometheus-2.18.1.linux-amd64.tar.gz```

If all is ok, then we can untar the gz archive.

``` tar xvfz prometheus-2.14.0.linux-amd64.tar.gz ```


Now CD into the folder

```cd prometheus-2.14.0.linux-amd64```

And start it

```./prometheus --config.file=prometheus.yml```

Prometheus should now be running.

You can visit it at http://[your ip address]:9090