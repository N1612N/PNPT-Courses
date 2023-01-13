
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
```