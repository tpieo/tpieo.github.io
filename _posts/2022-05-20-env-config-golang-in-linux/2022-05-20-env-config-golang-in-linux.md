---
title: "Environment Configuration: Golang in Linux"
categories: ["golang", "environment configuration"]
---

All command use sudo or in su mode.

1. Download installation.
```shell
wget https://go.dev/dl/go1.18.2.linux-amd64.tar.gz
```

2. Remove previous Go installation.
```shell
rm -rf /usr/local/go
```

3. Unzip installation.
```shell
tar -C /usr/local -xzf go1.18.2.linux-amd64.tar.gz
```

4. Add /usr/local/go/bin to the PATH environment variable.
```shell
vi /etc/profile
```
Add the below cmd into the file.
```shell
export PATH=$PATH:/usr/local/go/bin
```
execute /etc/profile.
```shell
source /etc/profile
```

5. Verify Go version
```shell
go version
```

6. You can config GOPROXY for downloading packages faster, for example:
```shell
go env -w GOPROXY=https://goproxy.cn,direct
```
<br>
Reference: <br>
[https://go.dev/doc/install](https://go.dev/doc/install)