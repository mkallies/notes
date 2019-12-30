# Bash 

## Text Manipulation 

- awk
- sed

- grep
String search

- sort
- uniq
- cat
- cut
- echo 
- fmt
- tr
- nl
- egrep
- fgrep
- wc

## Process Monitoring

- ps
- top
- htop
- atop
- lsof

## Network

- nmap
- tcpdump
- ping
- mtr
- traceroute
- airmon
- airodump
- dig
- iptables

## System Performance

- nmon
- isostat
- sar
- vmstat

## Other

- strace
- dtrace
- systemtap
- uname
- df
- history

Specify with a shebag at the top of the file

```
#!/bin/bash
```

Exit codes

1 - Catchall for general errors
2 - Misuse of shell builtins (according to Bash documentation)
126 - Command invoked cannot execute
127 - “command not found”
128 - Invalid argument to exit
128+n - Fatal error signal “n”
130 - Script terminated by Control-C
255\* - Exit status out of range
