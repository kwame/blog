---
title: "Ansible Create Local User"
date: 2023-01-19T08:39:31-06:00
draft: false
coverMeta: out
categories:
- DevOps
tags:
- devops
- linux
- open source
- ansible
---

### Ansible Create Local User

Ansible is a powerful automation tool that can help you manage and automate your infrastructure. One of the many things that Ansible can do is create and manage users, including the ability to add SSH keys for secure access. In this blog post, we will go over how to use Ansible to create a new user and add an SSH key for that user.

First, we need to create a new Ansible playbook. A playbook is a YAML file that contains instructions for Ansible on what tasks to execute. The playbook we will create will have two tasks: one to create the new user and one to add the SSH key for that user.

Here is an example playbook that creates a new user named "newuser" and adds an SSH key located at "~/.ssh/id_rsa.pub":
```
---
- name: Create new user
  user:
    name: newuser
    state: present
    generate_ssh_key: yes
    ssh_key_bits: 4096
    ssh_key_file: ~/.ssh/id_rsa.pub
```
The first task in this playbook uses the "user" module to create a new user named "newuser". The "state" parameter is set to "present" to ensure that the user is created if it does not already exist. The "generate_ssh_key" parameter is set to "yes" to generate an SSH key for the new user. The "ssh_key_bits" parameter is set to 4096 to specify the number of bits in the generated SSH key. The "ssh_key_file" parameter is set to "~/.ssh/id_rsa.pub" to specify the location of the SSH key.

Once you have created the playbook, you can run it with the following command:
```
ansible-playbook -i "localhost," -c local playbook.yml
```
This command tells Ansible to run the playbook on the localhost and create the user newuser with the ssh key specified.

In conclusion, Ansible is a powerful tool that can help you automate the creation and management of users, including the ability to add SSH keys for secure access. With just a few simple tasks in a playbook, you can easily create a new user and add an SSH key for that user.
