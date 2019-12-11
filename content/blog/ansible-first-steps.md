+++
title = 'Ansible First Steps'
date = 2019-12-11T15:25:03-06:00
draft = true
tags = ["ansible" "devops, sre, config management"]
description = "Desc"
+++

## Ansible intro
Ansible is a configuration management tool developed and maintained by RedHat. It can be used to install, remove, start, stop, restart and manage configuration files for services on your systems. 
Ansible can automate the state of a set of services and configuration files across an environment no matter the size of it. 
  Your infrastructure can be composed of a small set of servers or a large environment across different regions. 

### How it works
Ansible has 2 different node categories, the control node and the managed node. 
In the control node is where you will create the "Playbooks" that will be applied to your managed nodes. The connection is made via SSH, so no additional agents are needed to have communications between control and managed nodes. 
The most basic nomenclature of a Playbook will look like this:

```yaml
---
- name: MySQL server installed
  hosts: db_servers
  become: yes
```

