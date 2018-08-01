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
### "Dynamically" typed
```go
var data map[string]interface{}
err = json.Unmarshal([]byte(resp.Body()), &data)
// access data
var power = data["power"].(bool)
// access nested data
var cores = data["server"].(map[string]interface{})["cores"].(float64)
```
### Statically typed
```go
// TODO
```

## Building a CLI
```go
var rootCmd = &cobra.Command{
    Use:    "ServerControl",
}
var onCmd = &cobra.Command{
    Use:   "on",
    Short: "Power on",
    Long:  `Power on the Machine`,
    Run: func(cmd *cobra.Command, args []string) {
      Power(true)
    },
}
var resizeCmd = &cobra.Command{
    Use:   "resize",
    Short: "Resize Server",
    Long:  `Configure the number of cores and the amount of RAM. Server must be powered off!`,
    Run: func(cmd *cobra.Command, args []string) {
      Resize(cores, memory)
    },
}
    resizeCmd.Flags().IntVarP(&cores, "cores", "c", 1, "number of cores")
    resizeCmd.Flags().IntVarP(&memory, "memory", "m", 2, "amount of memory")
    resizeCmd.MarkFlagRequired("cores")
    resizeCmd.MarkFlagRequired("memory")
    rootCmd.AddCommand(onCmd)
    rootCmd.AddCommand(resizeCmd)
    if err := rootCmd.Execute(); err != nil {
        fmt.Println(err)
        os.Exit(1)
  }
```