# Everyone's Friend
Crypto, 200 points

## Description:
iykyk, amirite? rsa af. gl, hf. poctf2024.

p = 61
q = 53
n = 3233
e = 17
c = 264,889,119,374,559,357,870,453,4ce,264,77,a5d,87a,170,77,87a,b5a,a5d,119,87a,87a,b5a,2b2,170,96c,70a,77,7aa,870,b5a,6ed,170,5ec

## Solution: 
We write a Python script to compute phi and d (the decryption exponent) since we were given p and q. 

```python
from Crypto.Util.number import inverse

e = 17
n = 3233
# Convert C into a list of hex codes
c = [
    0x264, 0x889, 0x119, 0x374, 0x559, 0x357, 0x870, 0x453, 0x4ce,
    0x264, 0x77, 0xa5d, 0x87a, 0x170, 0x77, 0x87a, 0xb5a, 0xa5d,
    0x119, 0x87a, 0x87a, 0xb5a, 0x2b2, 0x170, 0x96c, 0x70a, 0x77,
    0x7aa, 0x870, 0xb5a, 0x6ed, 0x170, 0x5ec
]
p = 61
q = 53

phi = ( p -1 ) * (q - 1)
d = inverse(e, phi)

plaintext = ""
for i in c:
    m = pow(i, d, n)
    plaintext += chr(m)

print(plaintext)
```
[Script](./scripts/everyones_friend.py)

The flag: ``poctf{uwsp_7h3_h17chh1k3r5_6u1d3}``