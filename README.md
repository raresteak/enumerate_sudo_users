# enumerate_sudo_users
Enumerate users with sudo access on system
```
wget https://gist.githubusercontent.com/raresteak/ea537dc433c8f00cbd09c20e02c6c4fe/raw/c483f2eec536ecd9d8686ac7ddb7347a6b435ab5/enumerate_sudo_users -O /usr/local/sbin/enumerate_sudo_users && chmod 555 /usr/local/sbin/enumerate_sudo_users
```

```
#!/bin/bash

###############################################################################
#Script Name	: user_sudo_check
#Description	: Check which users on system can sudo with some form of
# 		  privileged access.
#Author		: Github raresteak
###############################################################################
[[ "$TRACE" ]] && set -x
[[ "$HEADER" ]] && echo "UserName,SystemName" # Useful for putting in a spreadsheet
main() {
if [[ $EUID -ne 0 ]]; then
  	echo "This script must be run as root" 
   	exit 1
fi
for user in $(compgen -u); do 
	(((sudo -l -U $user | grep "^User") | grep -v "not allowed") | awk {'print $2","$9'} ) | sed "s/://g"
done
}

main
```
Run script as root.

Sample output is username comma servername
```
root,server01
jackn,server01
dba,server01
printop,server01
```
