---
title: "Golang: File operation"
categories: ["Golang"]
---

Assume error has been handled.<br> 
Filename is **temp**, it is in the same directory.

## Read a file line by line
```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	file, err := os.Open("nim.asm")
	if err != nil {
		panic(err)
	}
	scanner := bufio.NewScanner(file)
	scanner.Split(bufio.ScanLines) // split by line
	for {
		success := scanner.Scan()
		if success == false { // Error or EOF will false
			err = scanner.Err()
			if err == nil {
				panic("Scan completed and reached EOF")
			} else {
				panic(err)
			}
		}
		fmt.Println(scanner.Text()) // Bytes() or Text()
	}
}
```
## Write bytes 
O_TRUNC will create a new file to write (verse O_APPEND)
```go
package main

import (
	"os"
)

func main() {
	// 可写方式打开文件
	file, err := os.OpenFile(
		"test.txt",
		os.O_WRONLY|os.O_TRUNC|os.O_CREATE,
		0666,
	)
	if err != nil {
		panic(err)
	}
	defer file.Close()
	byteSlice := []byte("Bytes!\n")
	_, err = file.Write(byteSlice)
	if err != nil {
		panic(err)
	}
}
```