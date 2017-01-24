+++
date = "2017-01-04T22:44:46-06:00"
title = "Puppet 4 server on CentOS 7 howto"
draft = true
tags = [
     "puppet",
     "centos",
     "linux",
     "devops",
]
categories = [
    "devops",
    "sysadmin",
    "linux",
]

menu = "main" 
+++

## Please take notice that this blog post is work in progress 

## What is Puppet?

Puppet is a tool for configuration management created by [Puppet Labs](https://puppet.com/) that enables system administrator to automate provisioning, configuration and management of a server infrastructure. A system administrator will always want to cut down on time spent repeating basic tasks, like installing packages, modifying configuration files, creating user account et al. Puppet can help with these kind of tasks. 
Once you understand the basics of Puppet and some other automation tools, you will have the ability to quickly deploy an infrastructure that has the same specs over and over. 

Here I will explain in very basic terms how to install Puppet 4 Open Source version in a server/agent setup using CentOS 7 (with SELinux enabled by the way). 

A Puppet server (CentOS 7 in this case) can manage different client nodes (or agents) from different OS's. In this setup we will not be using Passenger or any other runtime environment, in past Puppet versions, using passenger was the most commong recommendation. 


## Prerequisites

To follow this howto, you will need at least 2 VMs with root access to both of them. Make sure your VMs have the latest updates, so, just remember to do a "yum -y update && reboot" before starting installing and configuring packages on them. 

 * For the Puppet server, we will require at least 2.5 Gb of RAM memory. For the agent node, 1 Gb of RAM memory will be sufficient.  
 * To avoid the necessity of a local and private DNS server, we will rely on using the /etc/hosts file on both server and agent. 
 * We will need to open port 8140 on the Puppet server. You'll need to use some of your firewalld foo to work on this, if not, please look for my [Firewalld](http://http://informatux.net/blog/a%C3%B1o-nuevo-blog-nuevo/) howto.


## Example hosts setup

Hostname|RAM|HD
|------|------|-------|
|puppet.yourdomain.com|2.5 Gb|6 Gb| 
|p-client.yourdomain.com|1 Gb|6Gb| 

Puppet agent muy be installed on all hosts (including the Puppet server). 

## Install and configure Puppet Server

After you've created and updated the VM that will host the Puppet server, you will need to set the hostname to "puppet". As a note on Puppet Server, the initial configuration is set to use 2 Gb of RAM. 

    If you use a different name for the Puppet server, you'll need to adjust some configuration files, so, for the time being, please make sure to set the hostname to puppet.yourdomain.com. Otherwise, you'll get this error: *Error: Could not request certificate: The certificate retrieved from the master does not match the agent's private key*. Modifying the Puppet server FQDN configuration is beyond the scope of this howto.


Enable the oficial Puppet Labs collection repository:
   $ rpm -ivh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm

Install the puppetserver package:
   $ yum -y install puppetserver
