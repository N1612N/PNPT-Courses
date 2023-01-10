```sh
meterpreter>>
>> shell
# Information about Windows Defender [sc -> Service Control]
>>>  sc query windefend

# Information about All Service; Check for AV Services in the list
>>>  sc queryex type= service 

>>> netsh advfirewall firewall dump

>>> netsh firewall show state  

>>> netsh firewalll show config

```