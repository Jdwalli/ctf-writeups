# No Thing Lasts Forever
Crack, 100 Points

## Description:
Hold on... This can't be right...

My notes say this is supposed to be a "normal" crack challenge? So... I spend twelve weeks throwing these oddball cracking challenges at you, and after all that time we go back to wordlist and wait?

Kind of a jerk move, if you ask me.

## Solution:

We can use [JohnTheRipper (John)](https://www.openwall.com/john/) to help us crack the password to the archive.

First, we need to extract the hash from the archive using the following command:

```shell
zip2john Crack100-1.zip > hash.txt
```

This command generates a hash from the archive, which allows John to compare it against potential password hashes.

To verify the hash, we can display it:

```shell
cat hash.txt

txt:$zip2$*0*3*0*f8e6dc8ecc2d1eb264e8b8f67671c55f*93da*1f*fd8f6a6053dd133fbf9d03393ae02842ea25b4a3f495d42486ba1ff3f8edfe*d3e21765c8772b54f0e0*$/zip2$:flag.txt:Crack100-1.zip:Crack100-1.zip
```

We can then supply John a wordlist to compare against the hash and wait for the password to be cracked:
```shell
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt 

Using default input encoding: UTF-8
Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 128/128 ASIMD 4x])
Cost 1 (HMAC size) is 31 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
lol12345         (Crack100-1.zip/flag.txt)     
1g 0:00:00:07 DONE (2025-01-13 20:25) 0.1336g/s 10678p/s 10678c/s 10678C/s superm..Bulldog
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

Once we have the password, we can use 7z to extract the contents:

```shell
7z x Crack100-1.zip -p'lol12345' 

7-Zip 24.08 (arm64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-08-11
 64-bit arm_v:8-A locale=en_US.UTF-8 Threads:4 OPEN_MAX:1024

Scanning the drive for archives:
1 file, 231 bytes (1 KiB)

Extracting archive: Crack100-1.zip
--
Path = Crack100-1.zip
Type = zip
Physical Size = 231

Everything is Ok

Size:       31
Compressed: 231
```

After the flag is extracted, all we need to do is use ``cat`` to view its contents:

``cat flag.txt``


The flag: ``poctf{uwsp_7h3_hum4n_c0nd1710n}``


