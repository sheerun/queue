# Queue

[![GoDoc](https://godoc.org/github.com/sheerun/queue?status.svg)](https://godoc.org/github.com/sheerun/queue)
[![Release](https://img.shields.io/github/release/sheerun/queue.svg)](https://github.com/sheerun/queue/releases/latest)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](LICENSE.txt)

Lightweight, performant, thread-safe blocking FIFO queue based on auto-growing circular buffer.

## Usage

```go
q := New()

var wg sync.WaitGroup

wg.Add(2)

go func() {
  for i := 0; i < 10000; i++ {
    q.Append(i)
  }
  wg.Done()
}()

go func() {
  for i := 0; i < 10000; i++ {
    if q.Pop() != i {
      t.Errorf("Invalid returned index: %d", i)
      wg.Done()
      return
    }
  }
  wg.Done()
}()

wg.Wait()
```

## License

MIT
