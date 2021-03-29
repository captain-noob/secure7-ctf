# Cencode

### Encoded Flag : ``bcrjiomsbjvftepwvefvowmybxflkomqplkoebxlkblkbmdctqtjkyrjltqtnqjpgapwvdbvdpyjfxjpljwe``


## Decode

#### Enumeration

```bash

$ nc docker.h4x0rbox.com 3010
String to CEncode3 > a
lbnjwe
String to CEncode3 > b
ypbjwe
String to CEncode3 > A
ebxjwe
String to CEncode3 > 1
wijjwe
String to CEncode3 > {
jvfjwe
String to CEncode3 > 

```

*JWE*  is common

## Python Script to decode

```python

import re
import string
from pwn import *

  

proc = remote('docker.h4x0rbox.com',3010) # remote connection

  
chars = string.ascii_lowercase

chars += string.ascii_uppercase

chars +='0123456789~!@#$%^&*()_+=-}{][|.,?/`\\' # all to encode

  
  

enc_dict = {}

  

p = log.progress('')

for i in chars:

	p.status('Encoding with : '+i)

	proc.sendlineafter('String to CEncode3 >',i)

	encode = proc.recvline().decode('ascii').replace(" ",'').replace('\n','') # reading encoded string

	split = re.findall('...',encode)[0] # split into first 3 letters

	enc_dict[split] = i

p.success('Done ,Successfully Encoded')

  
  

chiper = "bcrjiomsbjvftepwvefvowmybxflkomqplkoebxlkblkbmdctqtjkyrjltqtnqjpgapwvdbvdpyjfxjpljwe"  #flag to decrypt

chiper_split = re.findall('...',chiper)

  

p = log.progress('')

decoded = []

for chips in chiper_split:

	p.status('Decoding : '+chips)

	decoded.append(enc_dict[chips]) 

	p.success('Decoded Successufully !')

flag=''.join(decoded)

log.success('Flag : '+flag)

```

#### Output

```bash

$ python bin/cencode.py 
[+] Opening connection to docker.h4x0rbox.com on port 3010: Done
[+] Done ,Successfully Encoded
[+] Decoded Successufully !
[+] Flag : SL7{Cust0m_mAppIngEncode3!}h
[*] Closed connection to docker.h4x0rbox.com port 3010

```

### Flag : `` SL7{Cust0m_mAppIngEncode3!}  ``