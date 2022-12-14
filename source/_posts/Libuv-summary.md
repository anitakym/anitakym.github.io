---
title: Libuv-summary
date: 2022-12-14 10:50:32
tags:
---
## 数据结构和通用逻辑
- https://libuv.org/
- https://github.com/thlorenz/libuv-dox/blob/master/types.md
```
Table of Contents generated with DocToc
- loop
uv_loop_t
- requests
uv_req_t
uv_getaddrinfo_t : uv_req_t
uv_shutdown_t : uv_req_t
uv_write_t : uv_req_t
uv_connect_t : uv_req_t
uv_udp_send_t : uv_req_t
uv_fs_t : uv_req_t
req->result
uv_work_t : uv_req_t
uv_connect_t : uv_req_t
- buffers
uv_buf_t
- handles
uv_handle_t
- streams
uv_stream_t : uv_handle_t
uv_tcp_t : uv_stream_t
uv_tty_t : uv_stream_t
uv_pipe_t : uv_stream_t
- udp
uv_udp_t : uv_handle_t
- poll
uv_poll_t : uv_handle_t
- prepare
uv_prepare_t : uv_handle_t
- idle
uv_idle_t : uv_handle_t
- async
uv_async_t : uv_handle_t
- timer
uv_timer_t : uv_handle_t
- process
uv_process_t : uv_handle_t
- file system
uv_fs_event_t : uv_handle_t
uv_fs_poll_t : uv_handle_t
- signal - uv_signal_t
- cpu info
uv_cpu_info_t
- interface address
uv_interface_address_t
- file info
uv_stat_t
uv_timespec_t
- stdio
uv_stdio_container_t
- process
uv_process_options_t
- enumerations
uv_errno_t
uv_handle_type
uv_req_type
uv_udp_flags
uv_poll_event
uv_stdio_flags
uv_process_flags
uv_fs_type
uv_fs_event
uv_fs_event_flags
```

## 事件循环


## 线程池和线程间通信


## 流机制


## C++胶水层把libuv功能引入JS