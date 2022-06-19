---
title: "Golang: Slice trap in append"
categories: ["golang"]
tags: "Golang"
---


```golang
s1 := []int{0, 1, 2}
s2 := append(s1[:0], s1[1:]...)
fmt.Println(s1)  //[1 2 2] this is the trap, I don't want to change s1
fmt.Println(s2)  //[1 2]
s1[0] = 666
fmt.Println(s1)  //[666 2 2] append will not make a new array
fmt.Println(s2)  //[666 2] 
```

Solution:
```golang
s1 := []int{0, 1, 2}
s2 := append(append(make([]int, 0, len(s1)), s1[:0]...), s1[1:]...)
fmt.Println(s1)  //[0 1 2] 
fmt.Println(s2)  //[1 2]
```
make a new array, we always append to the new array.