# Area51

## Downloading

```bash
$ wget http://ctf.h4x0rbox.com/files/6e447692e1b3ce91e46f3d755e3ad347/Area51.zip?token=eyJ1c2VyX2lkIjoxMDU5LCJ0ZWFtX2lkIjpudWxsLCJmaWxlX2lkIjoxMX0.YGBcRA.byHa_iW-G2neyfZQuQT3_bkW8BI  -O Area51.zip
```

## Unziping

```bash

$ unzip Area51.zip 
Archive:  Area51.zip
   skipping: Area51/secret.txt       unsupported compression method 99

$ 7z x Area51.zip                                                                                                                          [0/94675]

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_IN,Utf16=on,HugeFiles=on,64 bits,4 CPUs Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz (806E9),ASM,AES-NI)

Scanning the drive for archives:
1 file, 385 bytes (1 KiB)
                                                
Extracting archive: Area51.zip
--                 
Path = Area51.zip
Type = zip
Physical Size = 385                 
                                                
                           
Enter password (will not be echoed):
ERROR: Wrong password : Area51/secret.txt
                          
Sub items Errors: 1
                                                
Archives with Errors: 1                                                                                                                                                                           

Sub items Errors: 1
```

## Cracking Password

#### Hashing
```bash

$ /usr/sbin/zip2john Area51.zip  > hash
Area51.zip/Area51/ is not encrypted!
ver 1.0 Area51.zip/Area51/ is not encrypted, or stored with non-handled compression type
ver 2.0 efh 9901 Area51.zip/Area51/secret.txt PKZIP Encr: cmplen=53, decmplen=23, crc=7D0761C8



```

#### crack with john
```bash

$ john --wordlist=/usr/share/wordlists/rockyou.txt bin/hash 
Using default input encoding: UTF-8
Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 256/256 AVX2 8x])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
'princess101'      (Area51.zip/Area51/secret.txt)
1g 0:00:00:00 DONE (2021-03-28 16:18) 1.351g/s 22140p/s 22140c/s 22140C/s total90..cocoliso
Use the "--show" option to display all of the cracked passwords reliably
Session completed

```

### Password : ` princess101 `


## Extracting

```bash

$ 7z x Area51.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_IN,Utf16=on,HugeFiles=on,64 bits,4 CPUs Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz (806E9),ASM,AES-NI)

Scanning the drive for archives:
1 file, 385 bytes (1 KiB)

Extracting archive: Area51.zip
--
Path = Area51.zip
Type = zip
Physical Size = 385

    
Enter password (will not be echoed):
Everything is Ok          

Folders: 1
Files: 1
Size:       23
Compressed: 385
$ cat Area51/secret.txt 
'Sl7{AreY0u-In-Ar4a-51?}'

```

## Flag : `Sl7{AreY0u-In-Ar4a-51?}`