---
title: "How to add a Grafana Telegraf InfluxDB dashboard"
date: 2022-10-21T00:58:45-05:00
thumbnailImagePosition: top
thumbnailImage: img/grafana1.png
coverImage: img/grafana2.png
metaAlignment: center
coverMeta: out
categories:
- DevOps
tags:
- cover image
---

## How to add a Grafana pre-built dashboard 

Once you have configured your Grafana + InfluxDB + Telegraf host and you have confirmed that you are sending data, the next step you want to perform is to create a dashboard to display it's metrics.
These are the steps that you'll need to follow to install a pre-built Grafana dashboard.
We will be using the dashboard listed [here](https://grafana.com/grafana/dashboards/928-telegraf-system-dashboard/)

First you need to go to 
* Dashboards 
** Browse
![Grafana Dashboard 1](img/grafana-dashboard1.jpg)

In the following screen select 
* New
** Import 
![Grafana Dashboard 2](img/grafana-dashboard2.jpg)

In the "Import via grafana.com" field enter the ID of the dashboard and select "Load" 
![Grafana Dashboard](img/grafana-dashboard3.jpg)


In the following screen select the InlufxDB database name:
![Grafana Dashboard](img/grafana-dashboard4.jpg)


And finally you will have in the dashboards list the recently imported dashboard. 
![Grafana Dashboard](img/grafana-dashboard5.jpg)

