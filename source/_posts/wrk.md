---
title: wrk
date: 2021-06-10 18:16:01
tags:
---
https://github.com/wg/wrk

benchmarks 
```
#!/usr/bin/env bash

echo
MW=$1 USE_ASYNC=$2 node $3 &
pid=$!

sleep 2

wrk 'http://localhost:3333/?foo[bar]=baz' \
  -d 3 \
  -c 50 \
  -t 8 \
  | grep 'Requests/sec' \
  | awk '{ print "  " $2 }'

kill $pid

```