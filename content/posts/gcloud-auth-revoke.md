+++
title = 'Gcloud Auth Revoke'
date = 2018-10-19T21:16:09-05:00
draft = true
tags = ["tags"]
description = "Desc"

# For twitter cards, see https://github.com/mtn/cocoa-eh-hugo-theme/wiki/Twitter-cards
meta_img = "/images/image.jpg"

# For hacker news and lobsters builtin links, see github.com/mtn/cocoa-eh-hugo-theme/wiki/Social-Links
hacker_news_id = ""
lobsters_id = ""
+++
gcloud auth revoke [ACCOUNTS …] [--all] [GCLOUD_WIDE_FLAG …]


Revokes credentials for the specified user accounts or service accounts. When you revoke the credentials, they are removed from the local machine. If no account is specified, this command revokes credentials for the currently active account, effectively logging out of that account.

You can revoke credentials when you want to disallow access by gcloud and other Cloud SDK tools using a specified account. You don't need to revoke credentials to switch between accounts. 

```bash
kwame@r2d2:~$ gcloud auth revoke account1@email.com
Revoked credentials:
 - account1@email.com
     Credentialed Accounts
ACTIVE  ACCOUNT
*       account2@email.com
kwame@r2d2:~$ 
kwame@r2d2:~$ gcloud auth list
     Credentialed Accounts
ACTIVE  ACCOUNT
*       account2@email.com 

To set the active account, run:
    $ gcloud config set account `ACCOUNT`

kwame@r2d2:~$ 
```
