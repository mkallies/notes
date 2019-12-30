# Linux

## Virtualization

Running an OS within an OS and can scale with hardware.

Two types via hypervisor:
Type 1 - bare metal (your computer)
Type 2 - hosted (virtual machine & containers)

## Users & Groups

May need to use sudo:
```
# Create new user
useradd someuser

# Modify password
passwd someuser

# List users
cat /etc/passwd
```

Groups are important for security.

```
# Add a group
groupadd somegroup

# View groups
cat /etc/group

# Add user to a group
usermod -a -G somegroup someuser
```

## Permissions

```
# Display files/folders with their permissions

ls -l

drwxr-xr-x 1 mICHA 197609       0 Nov 13 08:02 '3D Objects'/
drwxr-xr-x 1 mICHA 197609       0 Jul 24 22:52  AppData/
lrwxrwxrwx 1 mICHA 197609      30 Jul 24 22:52 'Application Data' -> /c/Users/mICHA/AppData/Roaming/
```

rwx - read, write, execute

this is repeated three times

owner - group - everyone

7 rwx
6 rw-
5 r-x
4 r--
3 -wx
2 -w-
1 --x
0 ---

```
# Change permission on file
chmod 771 somefile.js

```

## Package Management

debian uses apt (advanced package tool)

redhat uses yum (yellowdog updater modified)

Use -y flag for auto yes
```
# Update repos
apt update -y

# Update packages
apt upgrade -y
```

## Process Management

```
ps

top

htop

# Use process number
kill 32832
```

## Memory & Storage

How to check memory
```
free -h

top

htop
```

How to check storage
```
# Filesystem
df -h

# Specified files & directories
du
```

## Networking

ifconfig

Loopback address (localhost)

```
tldr ping

tldr netstat

tldr arp
```

Linux DNS tools

dig
nslookup
whois
/etc/hosts
/etc/resolv.conf

HTTPS encryption provided by SSL/TSL

SSL - Secure Socket Layer
TLS - Transport Layer Security

SSL is deprecated, TLS is standard

Both use certificates that are NOT dependant on the protocol
