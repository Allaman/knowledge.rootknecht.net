---
title: Go
taxonomy:
    category:
        - golang
        - programming
    author:
        - Knecht
---

[TOC]

## Structs
```go
type status struct {
	status bool
	cores float64
	memory float64
}

s := status{power, cores, memory}
```

## Print formated string
```go
fmt.Printf("Current Status: Power %v, Cores %v, Memory %v", s.status, s.cores, s.memory)
```

## Format string without printing
```go
fmt.Sprintf("{\"cores\": %v}", cores)
```

## Rest GET
```go
resp, err := resty.R().
		SetHeaders(map[string]string{"Content-Type": "application/json", "X-Auth-UserId": userID,"X-Auth-Token": token}).
		Get(baseURL + endpoint)
```

## Load json data
### non statically typed
```go
var data map[string]interface{}
err = json.Unmarshal([]byte(resp.Body()), &data)
```