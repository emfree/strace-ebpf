Some initial experiments show that syscall tracing using eBPF has much lower
overhead than using strace:

```
$ sudo ./systrace & dd if=/dev/zero of=/dev/null bs=512 count=100k
[1] 12368
102400+0 records in
102400+0 records out
52428800 bytes (52 MB, 50 MiB) copied, 0.0509098 s, 1.0 GB/s

$ strace -c dd if=/dev/zero of=/dev/null bs=512 count=100k
102400+0 records in
102400+0 records out
52428800 bytes (52 MB, 50 MiB) copied, 4.63497 s, 11.3 MB/s
```

But we should also be able to stuff like include user stacks (which `strace`
doesn't) and humanize call arguments and return values (which `perf trace`
doesn't, as far as I know). Lots to do...
