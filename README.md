# Commands

- [Docker](#docker)
- [Git](#git)
- [Java](#java)
- [SSH](#ssh)


## Docker

```bash
# save image image-name
sudo docker save image-name | gzip > /tmp/image-name.img.gz
```

```bash
# load image image-name
gunzip -c /tmp/image-name.img.gz | sudo docker load 
```


## Git

```bash
# find which branches contain a commit
git branch --contains <commit>
```

```bash
# revert last commit and keep modified files
git reset --soft HEAD^
```


## Java

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

```bash
# enable JMX remote monitoring
java
  -Dcom.sun.management.jmxremote
  -Dcom.sun.management.jmxremote.port=9010
  -Dcom.sun.management.jmxremote.authenticate=false
  -Dcom.sun.management.jmxremote.ssl=false
  -Dcom.sun.management.jmxremote.local.only=false
  -jar app.jar
```

## SSH

```bash
# copy file from local to remote without scp
cat local.txt | ssh user@example.com "cat > /tmp/remote.txt"
```

```bash
# copy file from remote to local without scp
ssh user@example.com "cat /tmp/remote.txt" > local.txt
```

```bash
# SSH's X11 Forwarding (for instance xterm)
ssh -X user@example.com "xterm"

# the remote machine must have:
# 1. sshd X11 Forwarding enabled ("X11Forwarding yes" at /etc/ssh/sshd_config)
# 2. xorg-x11-xauth package installed (yum install xorg-x11-xauth)
```
