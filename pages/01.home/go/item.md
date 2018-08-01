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

## Rest
```go
import (
  "gopkg.in/resty.v1"
)
```
### Get
```go
resp, err := resty.R().
		SetHeaders(map[string]string{"Content-Type": "application/json", "X-Auth-UserId": userID,"X-Auth-Token": token}).
		Get(baseURL + endpoint)
if err != nil || resp.StatusCode() != 200 {
	// error handling
}
```

## net/http

```go
func Retrieve() map[string]interface{} {

	var urlBase = "https://example.com/v3/"
	var consumerKey = "325-2664324-67324"
	var accessToken = "960234-265623-3553"

	type Payload struct {
		ConsumerKey string `json:"consumer_key"`
		AccessToken string `json:"access_token"`
	}

	data := Payload{consumerKey, accessToken}
	payloadBytes, err := json.Marshal(data)
	if err != nil {
		panic(err)
	}
	body := bytes.NewReader(payloadBytes)

	req, err := http.NewRequest("POST", urlBase, body)
	if err != nil {
		panic(err)
	}
	req.Header.Set("Content-Type", "application/json")
	req.Header.Set("X-Accept", "application/json")

	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		panic(err)
	}

	defer resp.Body.Close()

	var items map[string]interface{}
	err = json.NewDecoder(resp.Body).Decode(&items)

	return items
}
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

**Result:**
```bash
Usage:
  ServerControl [command]

Available Commands:
  help        Help about any command
  off         Power off
  on          Power on
  resize      Resize Server
  status      Get status

Flags:
  -h, --help   help for ServerControl

Use "ServerControl [command] --help" for more information about a command.
```
**Source code**
```go
import (
  "github.com/spf13/cobra"
)
func main() {
    resizeCmd.Flags().IntVarP(&cores, "cores", "c", 1, "number of cores")
    resizeCmd.Flags().IntVarP(&memory, "memory", "m", 2, "amount of memory")
    resizeCmd.MarkFlagRequired("cores")
    resizeCmd.MarkFlagRequired("memory")
    rootCmd.AddCommand(onCmd)
    rootCmd.AddCommand(offCmd)
    rootCmd.AddCommand(resizeCmd)
    rootCmd.AddCommand(statusCmd)
    if err := rootCmd.Execute(); err != nil {
        fmt.Println(err)
        os.Exit(1)
  }
}

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
var offCmd = &cobra.Command{
    Use:   "off",
    Short: "Power off",
    Long:  `Power off the Machine`,
    Run: func(cmd *cobra.Command, args []string) {
      Power(false)
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
var statusCmd = &cobra.Command{
    Use:   "status",
    Short: "Get status",
    Long:  `Prints the current power status, number of cores and amount of memory of the Machine`,
    Run: func(cmd *cobra.Command, args []string) {
      PrintStatus()
    },
}
```