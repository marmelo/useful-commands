# Java

```bash
# get thread dump for PID 12345
jstack -l 12345 > /tmp/thread.log
```

```bash
# get heap summary for PID 12345
jmap -heap 12345 > /tmp/heap.log
```

```bash
# get heap histogram for PID 12345
jmap -histo 12345 > /tmp/histogram.log
```

```bash
# get heap dump for PID 12345
jmap -dump:format=b,file=/tmp/heap.bin 12345
```

```bash
# force garbage collection for PID 12345
jcmd 12345 GC.run
```
