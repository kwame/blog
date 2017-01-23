+++
date = "2017-01-22T22:24:01-06:00"
title = "fixing docker repo gpg key"

+++
Earlier today I was trying to download and apply the latest updates to my Debian system (which is a Debian GNU/Linux testing stretch), and when I was doing an apt-get update I was getting this error:

```bash
W: GPG error: https://apt.dockerproject.org/repo debian-stretch InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY F76221572C52609D
W: The repository 'https://apt.dockerproject.org/repo debian-stretch InRelease' is not signed.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

I went to the [oficial documentation site](https://docs.docker.com/engine/installation/linux/debian/) and all I was missing to do was a 
```bash
$ curl -fsSL https://yum.dockerproject.org/gpg | sudo apt-key add -
```
and that was all.

Hope this helps.
