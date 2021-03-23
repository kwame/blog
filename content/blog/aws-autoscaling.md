+++
title = 'AWS Autoscaling - Terraform style'
date = 2020-07-05T22:27:41-05:00
draft = true
tags = ["terraform"]
description = "describing process to create an autoscaling deployment in AWS using terraform"

# For twitter cards, see https://github.com/mtn/cocoa-eh-hugo-theme/wiki/Twitter-cards
meta_img = "/images/image.jpg"

# For hacker news and lobsters builtin links, see github.com/mtn/cocoa-eh-hugo-theme/wiki/Social-Links
hacker_news_id = ""
lobsters_id = ""
+++
In the past days I've been working with Terraform (v0.12.28) and I've spent some time deploying an AutoScaling environment.

- AWS cli https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html

In order to crate the AutoScaling deployment you will need to configure the following items:

- Launch Configuration
- Elastic Load Balancer
- EC2 ami
- Security Groups
- Auto Scaling Groups

Before jumping into the code, it's worth reviewing the recently added option to EC2, in the past, in order to create a AutoScaling deployment, you neded to create a Launch Configuration, but since (DATE) AWS added to the option list the Launch Templates option.
The Launch Templates does the following [link_here] and it's different like this from the Launch Configuration.

The first step is to write the code for the Launch Configuration.
The options needed in a Launch Configuration are the following
- name
- port
- ami
- other options

adding another line
