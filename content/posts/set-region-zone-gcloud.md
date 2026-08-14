+++
title = 'How to set a default region zone in Gcloud'
date = 2018-10-19T21:51:16-05:00
draft = false
tags = ["tags"]
description = "Desc"

# For twitter cards, see https://github.com/mtn/cocoa-eh-hugo-theme/wiki/Twitter-cards
meta_img = "/images/image.jpg"

# For hacker news and lobsters builtin links, see github.com/mtn/cocoa-eh-hugo-theme/wiki/Social-Links
hacker_news_id = ""
lobsters_id = ""
+++
This post is in context of setting up a k8s cluster. 
K8s requires a set of machines to host the k8s control plane and the worker nodes where containers are ultimately run.

```ruby
kwame@r2d2:~$ gcloud config set compute/region us-west1
Updated property [compute/region].
kwame@r2d2:~$ gcloud config set compute/zone us-west1-c
Updated property [compute/zone].
kwame@r2d2:~$ 

```
