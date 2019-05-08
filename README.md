# Log Watcher

[![Build Status](https://travis-ci.org/aravindavk/logwatcher.svg?branch=master)](https://travis-ci.org/aravindavk/logwatcher)

logwathcer运行期间，使用vim编辑log文件wq保存后，会加载该文件所有行内容；
logwatcher暂停，监控log4j实时日志，再启动logwathcer，暂停期间的日志会丢失。启动后的日志可实时watch到。

A [Rust](https://www.rust-lang.org/) library to watch the log files.

Note: Tested only in Linux

### Features:
1. Automatically reloads log file when log rotated
2. Calls callback function when new line to parse

### Usage

First, add the following to your `Cargo.toml`

```toml
[dependencies]
logwatcher = "0.1"
```

Add to your code,

```rust
extern crate logwatcher;
use logwatcher::LogWatcher;
```

Register the logwatcher, pass a closure and watch it!

```rust
let mut log_watcher = LogWatcher::register("/var/log/check.log".to_string()).unwrap();

log_watcher.watch(&|line: String| {
    println!("Line {}", line);
});
```
