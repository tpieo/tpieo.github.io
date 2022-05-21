---
title: "Golang: File operation"
categories: ["Golang"]
---

Assume error has been handled.<br> 
Filename is **temp**, it is in the same directory.

## Read all byte
```go
f, err := os.Open("temp")
b, err := ioutil.ReadAll(f)  // b is the all byte slice
```