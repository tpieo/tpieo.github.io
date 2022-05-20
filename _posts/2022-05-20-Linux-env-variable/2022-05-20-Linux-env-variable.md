---
title: Linux env variable
categories: ["Linux"]
---

Use **export** in terminal will create a temporary environmental variable for this terminal.
```shell
export PATH=$PATH:/usr/local/go/bin
```

Add the above cmd into **/etc/profile** file is for all users and permanent.<br>

And **source** it will take effect right now.
```shell
source /etc/profile
```