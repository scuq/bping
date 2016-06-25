# bping

bping (Bash Ping) is a simple bash script which pings multiple targets, every 2 seconds
with a timeout of 1 second, if every linux would use a ping/iputils version which supports the

```
       -O     Report outstanding ICMP ECHO reply before sending next packet.  This is useful together with the timestamp -D to
              log output to a diagnostic file and search for missing answers.

```

the world would be a better place, but thats a flight of fantasy.

## Features

- Ping multiple targets specified in a config-file
- Start the ping to each target in a seperate detached process
- Each process writes a logfile containing the target-ip and the current date in the filename (logpath configurable in the configfile)
- It rotates and restarts itself if a new day is detected
- Rotate can execute a post-rotatete-command, for example scp'ing yesterdays file to another host
- Default Packetsize is 1000, if the answers are truncated it switches to 56

## Logformat

`Year-Month-Day_Hour:Minute:Second [OK | NOT-OK] Source-Ip->Destination-Ip RTT (-10 if not available)`

Example:

```
2016-06-25_02:16:44 OK 10.20.1.104->8.8.8.8 37.8
2016-06-25_02:16:46 OK 10.20.1.104->8.8.8.8 36.3
2016-06-25_02:16:48 OK 10.20.1.104->8.8.8.8 36.6
2016-06-25_02:16:50 OK 10.20.1.104->8.8.8.8 35.2
2016-06-25_02:16:52 OK 10.20.1.104->8.8.8.8 36.6
2016-06-25_02:16:54 OK 10.20.1.104->8.8.8.8 37.9
```
