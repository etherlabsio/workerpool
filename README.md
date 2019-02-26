# workerpool
[![Build Status](https://travis-ci.org/etherlabsio/workerpool.svg)](https://travis-ci.org/etherlabsio/workerpool)
[![Go Report Card](https://goreportcard.com/badge/github.com/etherlabsio/workerpool)](https://goreportcard.com/report/github.com/etherlabsio/workerpool)
[![codecov](https://codecov.io/gh/etherlabsio/workerpool/branch/master/graph/badge.svg)](https://codecov.io/gh/etherlabsio/workerpool)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/etherlabsio/workerpool/blob/master/LICENSE)

Concurrency limiting goroutine pool. Limits the concurrency of task execution, not the number of tasks queued. Never blocks submitting tasks, no matter how many tasks are queued.

[![GoDoc](https://godoc.org/github.com/etherlabsio/workerpool?status.svg)](https://godoc.org/github.com/etherlabsio/workerpool)

This implementation builds on ideas from the following:

- http://marcio.io/2015/07/handling-1-million-requests-per-minute-with-golang
- http://nesv.github.io/golang/2014/02/25/worker-queues-in-go.html

## Installation
To install this package, you need to setup your Go workspace.  The simplest way to install the library is to run:
```
$ go get github.com/etherlabsio/workerpool
```

## Example
```go
package main

import (
	"fmt"
	"github.com/etherlabsio/workerpool"
)

func main() {
	wp := workerpool.New(2)
	requests := []string{"alpha", "beta", "gamma", "delta", "epsilon"}

	for _, r := range requests {
		r := r
		wp.Submit(func() {
			fmt.Println("Handling request:", r)
		})
	}

	wp.StopWait()
}
```
