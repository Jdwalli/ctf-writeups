# Put Down Thy Wrath
Crypto, 300 points

## Description:
In this challenge, you are given a public key and an encrypted message that was encrypted using a flawed implementation of homomorphic encryption. Your task is to analyze the encryption algorithm, identify its weaknesses, and use them to decrypt the message and reveal the flag. The provided file contains the encryption implementation, and here is the public key and the encrypted message. Good luck!

C:
79,74,3f,0f,5a,27,21,3a,36,48,64,51,64,0f,79,7e,1a,64,64,03,33,0f,64,64,57,21,27,3f,0f,2c,4a,3a,3f,24,27,3f,0f,7e,64,79,1a,64,2c

Public Key:
3233

NOTE: A deployment error has rendered this challenge arbitrary. No modifications will be made to this challenge.

## Solution:

```python
# homomorphic_encryption.py

import random
import binascii

class FlawedHomomorphicEncryption:
    def __init__(self, p, q):
        self.n = p * q
        self.p = p
        self.q = q
        self.public_key = self.n

    def encrypt(self, message):
        encrypted_message = []
        for char in message:
            m = ord(char)
            r = random.randint(1, self.n - 1)
            c = (m * r) % self.n
            encrypted_message.append(c)
        return encrypted_message

    def decrypt(self, encrypted_message):
        decrypted_message = []
        for c in encrypted_message:
            m = (c * pow(r, -1, self.n)) % self.n
            decrypted_message.append(chr(m))
        return ''.join(decrypted_message)

# Parameters (small primes for illustration; not secure)
p = 61
q = 53

# Create encryption object
encryption = FlawedHomomorphicEncryption(p, q)

# Flag message to encrypt
flag = "poctf{uwsp_T3mp357_4nd_7urnm01l}"

# Encrypt the flag
encrypted_message = encryption.encrypt(flag)

# Save public key and encrypted message
public_key = encryption.public_key
encrypted_message_hex = [binascii.hexlify(bytes([c])).decode() for c in encrypted_message]

with open("public_key.txt", "w") as pub_file:
    pub_file.write(str(public_key))

with open("encrypted_message.txt", "w") as enc_file:
    enc_file.write(','.join(encrypted_message_hex))

print(f"Generated homomorphic encryption and encrypted message.")
print(f"Public key saved to 'public_key.txt'.")
print(f"Encrypted message saved to 'encrypted_message.txt'.")
```

The flag was inside the code. 

The flag: ``poctf{uwsp_T3mp357_4nd_7urnm01l}``