```sh
meterpreter>>
>> shell

# check whoami 
>>>  whoami

# Check user privileges
>>>  whoami /priv

# Check group information
>>>  whoami /groups

# Check all users on the machine
>>> net user

# Get information about specific user
>>> net user <username>

# Get information about localgroups (expect to have error)  
>>> net localgroup 

# Alternate Command
>>> net localgroup <groupname: Administrators>

```