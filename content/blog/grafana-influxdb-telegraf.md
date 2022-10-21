---
title: "Grafana Influxdb Telegraf"
date: 2022-10-17T21:26:23-05:00
thumbnailImagePosition: top
thumbnailImage: img/grafana1.png
coverImage: img/grafana2.png
metaAlignment: center
coverMeta: out
categories:
- DevOps
- features
tags:
- cover image
---

Grafana - InfluxDB - Telegraf Linux Monitoring howto

**This is a quick tutorial to install Grafana, InfluxDB and Telegraf on a Debian based system**

Grafana has recently become one of the preferred tools for data visualization, this tool provides the users with the required tooling to display data via charts and graphs and these can be unified into one dashboard.

InfluxDB is a time series database. This means that it's a collection of observations of well-defined data items resulted through repeated measurements over time. Time series data is indexed in time order which is a sequence of data points.

Telegraf is a server based agent used for collecting (or scraping) metrics from the host.
<br/><br/>
### 1. Install grafana

```
$ apt-get install -y apt-transport-https wget
$ wget -q -O /usr/share/keyrings/grafana.key https://packages.grafana.com/gpg.key
$ echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
$ apt-get update && apt-get -y install grafana
$ systemctl daemon-reload
$ systemctl start grafana-server
$ systemctl enable grafana-server
$ systemctl status grafana-server
$ netstat -luntp | grep 3000
``` 

Now you should be able to go to http://ip.of.your.host:3000 and login to Grafana

### 2. Install InfluxDB

```
$ wget -q https://repos.influxdata.com/influxdb.key
$ echo '23a1c8836f0afc5ed24e0486339d7cc8f6790b83886c4c96995b88a061c5bb5d influxdb.key' | sha256sum -c && cat influxdb.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdb.gpg > /dev/null
$ echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdb.gpg] https://repos.influxdata.com/debian stable main' | sudo tee /etc/apt/sources.list.d/influxdata.list
$ apt-get update && apt-get -y install influxdb
$ systemctl start influxdb.service
$ systemctl status influxdb.service
$ systemctl enable influxdb.service
$ netstat -luntp | egrep '8086|8088'
```


### 3. Install Telegraf

```
$ wget -qO- https://repos.influxdata.com/influxdb.key | sudo tee /etc/apt/trusted.gpg.d/influxdb.asc >/dev/null
$ source /etc/os-release
$ echo "deb https://repos.influxdata.com/${ID} ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
$ apt-get update && sudo apt-get -y install telegraf
$ cp /etc/telegraf/telegraf.conf /etc/telegraf/telegraf.conf.orig
$ telegraf -sample-config -input-filter cpu:mem:disk -output-filter influxdb > /etc/telegraf/telegraf.conf
$ systemctl start telegraf.service
$ systemctl status telegraf.service
$ systemctl enable telegraf.service
```

You can use this telegraf.conf config to monitor your Linux host:

```
[global_tags]
[agent]
  interval = "10s"
  round_interval = true
  metric_batch_size = 1000
  metric_buffer_limit = 10000
  collection_jitter = "0s"
  flush_interval = "10s"
  flush_jitter = "0s"
  precision = "0s"
  hostname = ""
  omit_hostname = false

[[outputs.influxdb]]

###############################################################################
#                            INPUT PLUGINS                                    #
###############################################################################

# Read metrics about cpu usage
[[inputs.cpu]]
  percpu = true
  totalcpu = true
  collect_cpu_time = false
  report_active = false
  core_tags = false

[[inputs.disk]]
  mount_points = ["/"]
  ignore_fs = ["tmpfs", "devtmpfs", "devfs", "iso9660", "overlay", "aufs", "squashfs"]

[[inputs.mem]]
[[inputs.system]]
[[inputs.processes]]
[[inputs.swap]]
[[inputs.diskio]]
[[inputs.io]]
[[inputs.filestat]]
[[inputs.net]]
[[inputs.net_response]]
[[inputs.netstat]]
[[inputs.procstat]]
pattern = "httpd|java|python|telegraf|tomcat8|htop|apache2|www-data"
user = "daemon|root|telegraf|www-data|tomcat8"
[[inputs.sysstat]]
[[inputs.kernel]]
```

After the install process of Grafana, InfluxDB and Telegraf has been completed, the next step is to create a graph and dashboard to display the data collected from the Linux host. 

