---
title: "Golang: Connect Mysql"
categories: ["golang"]
---

# Connect
```go
package main

import (
	"database/sql"
	"fmt"

	_ "github.com/go-sql-driver/mysql"
)

var db *sql.DB

func init() {
	var err error
	//format: username:password@protocal(host:port)/database
	db, err = sql.Open("mysql", "root:123456@tcp(127.0.0.1:3306)/atguigudb")
	if err != nil {
		//check if the format is right, it won't check username and password
		panic(err)
	}
	if err := db.Ping(); err != nil {
		//check if username and password right
		panic(err)
	}
	fmt.Println("Connected")
}

func main() {
	db.Close()
}
```
# Select
## QueryRow
```go
// single result, Scan will close connection
var m string
sql := "select first_name from employees"
db.QueryRow(sql).Scan(&m)
```
## Query
```go
// multiple results, need rows.Close()
var m string
sql := "select first_name from employees"
rows, err := db.Query(sql)
if err != nil {
	panic(err)
}
for rows.Next() {
	if err := rows.Scan(&m); err != nil {
		fmt.Println(err)
	}
	fmt.Println(m)
}
rows.Close()
```
# Exec
```go
sql := "insert into dept values (88, 88, 88);"
if _, err := db.Exec(sql); err != nil {
	fmt.Println(err)
}
```
# Other
```go
db.SetMaxOpenConns(100)
db.SetMaxIdleConns(10)
```