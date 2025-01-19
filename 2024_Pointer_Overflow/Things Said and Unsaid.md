# Things Said and Unsaid
Stego, 100 points

## Description:
So there I was connected to the free McDonald's Wi-Fi hackin' the ISS nav computer as it passed by from orbit and I intercepted a still image from one of the onboard camera feeds. Something about it just seems a little odd, but I can't quite place it... Then again, it might just be my face-blindness acting up!

Remember, this is a Stego challenge. A password will be required to solve the challenge, and that means the password will also be hidden somewhere in the challenge.

![Image](images/Stego100-3.jpeg)

## Solution:

Running ``file`` on the image yields nothing so we can use ``binwalk -e`` to extract any hidden data: 

```shell
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
562069        0x89395         Zip archive data, encrypted compressed size: 57, uncompressed size: 29, name: Stego100-3_flag.txt
562298        0x8947A         End of Zip archive, footer length: 22
```

After extracting, running the ``file`` command on the zip archive reveals an encrypted archive:  

```shell
89395.zip: Zip archive data, at least v5.1 to extract, compression method=AES Encrypted
```

According to the description, the password is hidden in the file. Running the ```strings``` command on the image reveals: 

```shell
.......
sHEXa
k&W?
Oi%q
Stego100-3_flag.txt
czN*
probably_improbable
```

We can now use ``probably_improbale`` as a password for the zip file. After unzipping the file we can view the flag.

The flag: ``poctf{uwsp_w3_4r3_such_57uff}``