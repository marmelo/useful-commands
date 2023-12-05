# Commands

- [Bash](#bash)
- [Docker](#docker)
- [Git](#git)
- [Java](#java)
- [Mail](#mail)
- [Nmap](#nmap)
- [PostgreSQL](#postgresql)
- [SSH](#ssh)
- [Tmux](#tmux)
- [Tor](#tor)
- [YouTube](#youtube)


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

## Mail

```bash
# test smtp server
swaks -s server -f from -t to -au user -ap pass
```

## Nmap

```bash
# scan open ports
nmap 192.168.1.1
```

```bash
# scan open ports with service info
nmap -sV 192.168.1.254
```

```bash
# scan subnet for devices
nmap -sn 192.168.1.1-255
nmap -sn 192.168.1.1/24
```

```bash
# scan subnet for ports
nmap -p22,80,443 192.168.1.1/24
```

```bash
# scan subnet for ports with service info
nmap -sV -p22,80,443 192.168.1.1/24
```

```bash
# reverse lookup subnet
nmap --dns-servers 8.8.4.4,8.8.8.8 -sL 209.132.183.105/24
```


## PostgreSQL

```sql
# show running queries
SELECT procpid, age(clock_timestamp(), query_start), usename, current_query 
FROM pg_stat_activity 
WHERE current_query != '<IDLE>' AND current_query NOT ILIKE '%pg_stat_activity%' 
ORDER BY query_start desc;
```

```sql
# terminate connections
SELECT pg_terminate_backend(pg_stat_activity.pid)
FROM pg_stat_activity
WHERE pg_stat_activity.datname = '<database name>';
```

```sql
# copy database
CREATE DATABASE "new" WITH TEMPLATE "old";
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

```bash
# SSH socks5 proxy
ssh -D 9050 user@domain.com

curl --socks5 127.0.0.1:9050 ipinfo.io
proxychains curl ipinfo.io
proxychains firefox
```

## Tmux

```bash
# create named session
tmux new -s session-name
```

```bash
# dettach session (inside tmux)
Ctrl+b d
```

```bash
# list session
tmux ls
```

```bash
# attach session
tmux attach -t session-name
tmux attach -t 0
```

```bash
# windows
Ctrl+b c Create a new window (with shell)
Ctrl+b w Choose window from a list
Ctrl+b 0 Switch to window 0 (by number )
Ctrl+b , Rename the current window
```

```bash
# panes
Ctrl+b % Split current pane horizontally into two panes
Ctrl+b " Split current pane vertically into two panes
Ctrl+b o Go to the next pane
Ctrl+b ; Toggle between the current and previous pane
Ctrl+b x Close the current pane
```


## Tor

```bash
# create Tor connection to explicit country exit node
echo -e "ExitNodes {us}\nStrictNodes 1" | tor -f -
```

```bash
# use curl
curl --socks5 127.0.0.1:9050 ipinfo.io
```

```bash
# use torsocks
torsocks curl ipinfo.io
```

```bash
# use proxychains
proxychains curl ipinfo.io
```

```bash
# use chromium
chromium --user-data-dir=/tmp/x --proxy-server="socks5://127.0.0.1:9050"
```

## YouTube

```bash
# download playlist to mp3
youtube-dl -x --audio-format="mp3" --audio-quality="160k" --add-metadata --continue "https://www.youtube.com/playlist?list=PL7x1NEEwqJNvSGCXac6zGxERF9CDcsOK9"
```
