# End of the Line
Reverse, 100 points

## Description:
I got into CTFs a long time ago. Despite that, I remember how tough it was. It seemed impossible to solve all of the challenge. Heck, it seemed impossible to solve one. I remember how intimidating it was, but I also remember how amazing it felt to solve my first challenge and submit my first flag.

Looking back, it wasn't a tough challenge, but it was a start. Well, here's your chance. This is a recreation of the very first CTF challenge I solved. If you manage to solve this one, just remember that this is where I started, too.

## Solution:
Running the program asks us for a password so we need to look inside the binary to figure out the correct password.

If we run the command ``strings ./Reverse100-2`` we can easily see parts of the flag

```shell
H=0@@
poctf{uwH
sp_d0_0rH
p_d0_0r_H
d0_n07}
```

If we put it together, we can get the actual flag.

The flag: ``poctf{uwsp_d0_0r_d0_n07}``