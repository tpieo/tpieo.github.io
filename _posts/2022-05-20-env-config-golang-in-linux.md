---
title: "env config: golang in linux"
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
export PATH=$PATH:/usr/local/go/bin
```

5. Verify Go version
```shell
go version
```

6. You can config GOPROXY for downloading packages faster, for example:
```shell
go env -w GOPROXY=https://goproxy.cn,direct
```