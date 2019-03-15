# enumerate_sudo_users
Enumerate users with sudo access on system.

I needed a quick script to run across servers in a datacenter that would tell me which users had sudo access on systems.  I made the assumption that if a user could run commands via sudo they had some degree of privileged access.  Thus providing a list of who on which system.

Run script as root.

Sample output is username comma servername
```
root,server01
jackn,server01
dba,server01
printop,server01
```
