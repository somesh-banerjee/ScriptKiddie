# Enumeration

```
nmap -sC -sV -p 1-10000 <ip>
```
-sC: to perform default script scans\
-sV: Probe open ports to determine service/version info\
-p: ports to scan

We can also use the following which only scans open ports.
```
ports=$(nmap -p- --min-rate=1000 -T4 <ip> | grep ^[0-9] | cut -d '/' -f
1 | tr '\n' ',' | sed s/,$//)
nmap -sC -sV -p$ports <ip>
```

# Stabilize nc shell

After getting a reverse shell by listening on any port using `nc -lvnp <port>` We can get upgrade the shell by performing the following
1. Run `python -c 'import pty;pty.spawn("/bin/bash")'`. If this gives error like "python dont exist" use python2 or python3 instead.

Just by using this we will get a comparatively better shell. But we can't use autocomplete and arrow keys. For more stable shell

2. Run `export TERM=xterm` in reverse shell and background the process with Ctrl + Z.
3. Run `stty raw -echo; fg` in your own terminal. This will give the stable shell.

Also there is another technique using socat.
