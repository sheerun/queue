# Queue

[![GoDoc](https://godoc.org/github.com/sheerun/queue?status.svg)](https://godoc.org/github.com/sheerun/queue)
[![Release](https://img.shields.io/github/release/sheerun/queue.svg)](https://github.com/sheerun/queue/releases/latest)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](LICENSE.txt)

Lightweight, tested, performant, thread-safe, blocking FIFO queue based on auto-resizing circular buffer.

## Usage

```go
package main

import (
  "fmt"
  "sync"
  "time"

  "github.com/sheerun/queue"
)

func main() {
  q := queue.New()
  var wg sync.WaitGroup
  wg.Add(2)

  // Worker 1
  go func() {
    for i := 0; i < 500; i++ {
      item := q.Pop()
      fmt.Printf("%v\n", item)
      time.Sleep(10 * time.Millisecond)
    }
    wg.Done()
  }()

  // Worker 2
  go func() {
    for i := 0; i < 500; i++ {
      item := q.Pop()
      fmt.Printf("%v\n", item)
      time.Sleep(10 * time.Millisecond)
    }
    wg.Done()
  }()

  for i := 0; i < 1000; i++ {
    q.Append(i)
  }

  wg.Wait()
}

```

## License

MIT
