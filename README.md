# enumerate_sudo_users
Enumerate users with sudo access on system
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
