# Math

```bash
$ nc docker.h4x0rbox.com 5020
Have You done your Homework
Score 522+ to get your surprise.
x = 54%34
x = 


```


## Exploit.py

```python


from pwn import *

proc = remote('docker.h4x0rbox.com',5020) #connecting to server

proc.recvline() #read 1st line 
proc.recvline() #read 2nd line

while True: #if false throw error with flag
	value = proc.recvline() #read question
	value = value.decode('ascii') 
	#log.info('Calculate : '+value) 
	value = value.split('=')\[-1\] 
	value = eval(value) #calculating value
	proc.sendline(str(value)) #sending calculated value 
	value = proc.recvline() 
	value = value.decode('ascii').split(':')\[-1\]
	log.success('Your Score is :'+value) #print score

proc.interactive()


```

## Exploit
```bash

[+] Your Score is :  517
[+] Your Score is :  518
[+] Your Score is :  519
[+] Your Score is :  520
[+] Your Score is :  521
[+] Your Score is :  522
[+] Your Score is :x = Congratulations You Deserve Flag.
Traceback (most recent call last):
  File "math.py", line 14, in <module>
    value = eval(value)
  File "<string>", line 1
    'SL7{MaTHl0V3R!}'
       ^
SyntaxError: invalid syntax
(guru@blackspades)-[~/Desktop/secure7/ctf]$ 


```


## Flag : ` SL7{MaTHl0V3R!} `

