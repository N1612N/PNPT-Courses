## Executables

### WinPEAS 
[https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS)

```sh
 meterpreter>> 
 >> cd c:\\windows\tmp
 >> upload <~/path/to/winPeasfile>
 >> pwd
 >> 
 >> shell
 >>> winPEAS.exe
 
 # if nothing happens after running, check .net version support in the windows. This script wont work if the machine doesnt support dotnet v4.
```

### Seatbelt 
[https://github.com/GhostPack/Seatbelt](https://github.com/GhostPack/Seatbelt)

### Watson 
[https://github.com/rasta-mouse/Watson](https://github.com/rasta-mouse/Watson)

### SharpUp 
[https://github.com/GhostPack/SharpUp](https://github.com/GhostPack/SharpUp)


## PowerShell

### Sherlock 
[https://github.com/rasta-mouse/Sherlock](https://github.com/rasta-mouse/Sherlock)

### PowerUp 
[https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc)
```sh
meterpreter>> 
>> shell
>>> powershell -p bypass
# if the session hangs or dont response, then its windows blicking the powershell from running. Might have to restart the session.

# Alternate method to run powershell using metasploit.
Meterpreter>>
>> load powershell
# try to get powershell this way. if this fails then windows will be blocking it.

# Powesploit commands not added. Add later.
```

### JAWS 
[https://github.com/411Hall/JAWS](https://github.com/411Hall/JAWS)


## Others

### Windows Exploit Suggester 
[https://github.com/AonCyberLabs/Windows-Exploit-Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)
```sh

meterpreter>>
>> shell
>> systeminfo
# Copy the systeminfo of victim mahine and save it ina text file to feed it to exploit suggester later.


# Clone the repository from github to local machine<attacker machine>

# Update the tool
> ./windows-exploit-suggester.py --update
# After update, current database (dbname-mssb.xls) will be printed out in the output. will have to use later.

# upgrade the xlrd
> pip install xlrd --upgrade

>./windows_exploit_suggester.py --database <current db-mssb.xls> --systeminfo <sysinfofile.txt>
```

### Metasploit Local Exploit Suggester 
[https://blog.rapid7.com/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/](https://blog.rapid7.com/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/)
```sh
meterpreter>>
>> run post/multi/recon/local_exploit_suggester

# Ta Da !! 
# Copy and keep all the exploitable vulnerabilities from metasploit exploit suggester in a file for later use.

# also save the system information in a text file for later use.

>> shell
>> systeminfo
```

## Checklist

### Windows PrivEsc Checklist 
[https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation](https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation)