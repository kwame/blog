+++
title = 'How to create a bare git repo'
date = 2018-10-04T00:54:38-05:00
draft = false
tags = ["tags"]
description = "Desc"
+++

## What is Git?
Git is a version-control system for tracking changes in computer files and coordinating work on those files among multiple people. It is primarily used for source-code management in software development, but it can be used to keep track of changes in any set of files

To align with best practices, it is recommended to store all your code in version control. This will help you to modify, restore and reproduce your project with less effort. 

### Initializing a new repository
For this tutorial, I will be using the same Linux instance as server and client.

The first step you need to perform is decide in which directory you want to store your git repo, here I will be using /opt.

  * Create a directory in which you will store your git repo

```ruby
root@k8s-master:~# cd /opt/code/
root@k8s-master:/opt/code# 
root@k8s-master:/opt/code# mkdir project.git
root@k8s-master:/opt/code# 
root@k8s-master:/opt/code# cd project.git/
root@k8s-master:/opt/code/project.git#
```

  * Now initialize the git repository

```ruby
root@k8s-master:/opt/code/project.git# git init --bare
Initialized empty Git repository in /opt/code/project.git/
root@k8s-master:/opt/code/project.git# ls -lhtr
total 32K
drwxr-xr-x 4 root root 4.0K Oct  6 22:21 refs
drwxr-xr-x 2 root root 4.0K Oct  6 22:21 hooks
drwxr-xr-x 2 root root 4.0K Oct  6 22:21 info
-rw-r--r-- 1 root root   73 Oct  6 22:21 description
drwxr-xr-x 2 root root 4.0K Oct  6 22:21 branches
drwxr-xr-x 4 root root 4.0K Oct  6 22:21 objects
-rw-r--r-- 1 root root   23 Oct  6 22:21 HEAD
-rw-r--r-- 1 root root   66 Oct  6 22:21 config
root@k8s-master:/opt/code/project.git# 
```

  * Now modify the permissions on the directory. 

The code is stored under the user's kwame home directory.
The user kwame is part of the "repo" group.
I will modifiy the permissions on the /opt/code/project.git directory so all members of the "repo" group can read and write to it.

```ruby
root@k8s-master:/opt/code# chgrp -R repo project.git/
root@k8s-master:/opt/code# chmod 775 project.git/
root@k8s-master:/opt/code# ls -lhtr project.git/
total 32K
drwxrwxr-x 4 root repo 4.0K Oct  6 22:21 refs
drwxrwxr-x 2 root repo 4.0K Oct  6 22:21 hooks
drwxrwxr-x 2 root repo 4.0K Oct  6 22:21 info
-rwxrwxr-x 1 root repo   73 Oct  6 22:21 description
drwxrwxr-x 2 root repo 4.0K Oct  6 22:21 branches
drwxrwxr-x 4 root repo 4.0K Oct  6 22:21 objects
-rwxrwxr-x 1 root repo   23 Oct  6 22:21 HEAD
-rwxrwxr-x 1 root repo   66 Oct  6 22:21 config
root@k8s-master:/opt/code# 

```

  * The next step is to add your code to the bare repo.

```ruby
[kwame@k8s-master ~]$ git clone /opt/code/project.git/
Cloning into 'project'...
warning: You appear to have cloned an empty repository.
done.
[kwame@k8s-master ~]$ 

```

  * Change to the cloned directory and add a file

```ruby
[kwame@k8s-master ~]$ cd project/
[kwame@k8s-master project]$ vim file1
[kwame@k8s-master project]$ 
```

  * Configure your git user settings

```ruby
[kwame@k8s-master project]$ git config user.email kwame@informatux.net
[kwame@k8s-master project]$ git config user.name "Kwame Bahena"
[kwame@k8s-master project]$ git config user.email
kwame@informatux.net
[kwame@k8s-master project]$ git config user.name
Kwame Bahena
[kwame@k8s-master project]$ 
```


  * Now add the file to the repo and perform the initial commit

```ruby
[kwame@k8s-master project]$ git add file1
[kwame@k8s-master project]$ git commit -am "initial commit"
[master (root-commit) 0282cc8] initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 file1
[kwame@k8s-master project]$ 
```

  * Now push your code to the repo

```ruby
[kwame@k8s-master project]$ git push origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 230 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To /opt/code/project.git/
 * [new branch]      master -> master
[kwame@k8s-master project]$ 
```


 * At this stage, other users can now clone, modify and add more files to this repo.


```ruby
[ansible@k8s-master ~]$ git clone /opt/code/project.git/
Cloning into 'project'...
done.
[ansible@k8s-master ~]$ cd project/
[ansible@k8s-master project]$ ls -lhtr
total 4.0K
-rw-rw-r-- 1 ansible ansible 20 Oct  6 22:39 file1
[ansible@k8s-master project]$ git config user.name "ansible"
[ansible@k8s-master project]$ git config user.email "ansible@informatux.net"
[ansible@k8s-master project]$ vim file1 
[ansible@k8s-master project]$ git commit -am "adding information to file1"
[master f3d2a53] adding information to file1
 1 file changed, 2 insertions(+)
[ansible@k8s-master project]$ git push
Counting objects: 5, done.
Writing objects: 100% (3/3), 277 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To /opt/code/project.git/
   0282cc8..f3d2a53  master -> master
[ansible@k8s-master project]$ 
```

  * Now I'll switch to my user kwame and perform a git pull to get the latest code

```ruby
[kwame@k8s-master ~]$ cd project/
[kwame@k8s-master project]$ git pull
remote: Counting objects: 5, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From /opt/code/project
   0282cc8..f3d2a53  master     -> origin/master
Updating 0282cc8..f3d2a53
Fast-forward
 file1 | 2 ++
 1 file changed, 2 insertions(+)
[kwame@k8s-master project]$ cat file1 
This is a test file

Added an extra file

[kwame@k8s-master project]$ 
```


These are the steps that you'll need to follow in order to create a local repo and collaborate with other users.


