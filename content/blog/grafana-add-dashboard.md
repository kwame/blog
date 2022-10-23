---
title: "How to add a Grafana Telegraf InfluxDB dashboard"
date: 2022-10-21T00:58:45-05:00
thumbnailImagePosition: top
thumbnailImage: img/dashboard-head.png
coverImage: img/dashboard.png
metaAlignment: center
coverMeta: out
categories:
- DevOps
tags:
- devops
- linux
- open source
---

## How to add a Grafana pre-built dashboard 

Once you have configured your Grafana + InfluxDB + Telegraf host and you have confirmed that you are sending data, the next step you want to perform is to create a dashboard to display it's metrics.
These are the steps that you'll need to follow to install a pre-built Grafana dashboard.
We will be using the dashboard listed [here](https://grafana.com/grafana/dashboards/928-telegraf-system-dashboard/)

First you need to go to 
- Dashboards 
  - Browse
![This is an image](http://informatux.net/img/grafana-dashboard1.png)

In the following screen select 
- New
  - Import 
![This is an image](http://informatux.net/img/grafana-dashboard2.png)

In the "Import via grafana.com" field enter the ID of the dashboard and select "Load" 
![This is an image](http://informatux.net/img/grafana-dashboard3.png)


In the following screen select the InlufxDB database name:
![This is an image](http://informatux.net/img/grafana-dashboard4.png)


And finally you will have in the dashboards list the recently imported dashboard. 
![This is an image](http://informatux.net/img/grafana-dashboard5.png)

