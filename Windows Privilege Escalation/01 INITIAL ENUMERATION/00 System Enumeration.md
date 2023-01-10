```sh
meterpreter>>
>> shell

# To get the detailed system info
>>> systeminfo

# To get specific information about the system
>>> systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type" 

# Get the hostname
>>> hostname

# Its a good idea to check the patch info of system
>>> wmic qfe #windows management instrumentation commandline quick fix engineering

# To get a tailored output than the long wide output
>>> wmic qfe get Caption,Description,HotFixID,InstalledOn
# check the Knowledge Base (KB65456465) in the output and know about hot patches in the system

# To get the system disk information
>>> wmic logicaldisk

# Better View
>>> wmic qfe get Caption,Description,Providername
```