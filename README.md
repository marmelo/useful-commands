# Commands

- [Bash](#bash)
- [Docker](#docker)
- [Git](#git)
- [Java](#java)
- [SSH](#ssh)
- [Tor](#tor)


## Bash

```bash
# forward port without iptables
socat TCP4-LISTEN:8080,fork TCP4:1.1.1.1:8080
```

```bash
# create a RAM disk
mount -t tmpfs -o size=512m tmpfs /mnt/tmpfs
```

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


## HTTP

``` bash
# perform 1000 HTTP requests using 5 concurrent threads
ab -n 1000 -c 5 http://localhost:8080/api/version

# this requires Apache HTTP server benchmarking tool which is available though
# package httpd-tools in RHEL/CentOS and apache2-utils in Debian/Ubuntu
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

```
# SSH socks5 proxy
ssh -D 9050 user@domain.com

curl --socks5 127.0.0.1:9050 ipinfo.io
proxychains curl ipinfo.io
proxychains firefox
```


## Tor

```bash
# create Tor connection to explicit country exit node
echo -e "ExitNodes {us}\nStrictNodes 1" | tor -f -

# use curl
curl --socks5 127.0.0.1:9050 ipinfo.io

# use torsocks
torsocks curl ipinfo.io

## use proxychains
proxychains curl ipinfo.io
```
