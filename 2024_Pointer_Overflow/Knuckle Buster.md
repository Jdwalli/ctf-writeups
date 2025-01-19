# Knuckle Buster
Crypto, 200 points

## Description:
In this challenge, two individuals—Alice and Bob—are communicating in secret. They use the Diffie-Hellman key exchange protocol to protect their communication. I will provide you with enough information to decrypt a message intercepted between them. All you need to do is calculate the shared secret and decrypt it to get the flag.

Here is the encrypted flag. It was encrypted using AES-256-CBC, with SHA-256 for key derivation and a prepended 16 byte IV.

publicA
-----BEGIN PUBLIC KEY-----
MIGaMFMGCSqGSIb3DQEDATBGAkEAiBB/FlC3W8aPLJxYGXzKsnpEmPKIKR4JetlA1ky+TKTYofXUKSFucGxtrmWlVFjnLZUqJFjj0bVDKSiYOfod1wIBAgNDAAJAN3YrjXtIssyugO9tQ3BRy2TN92Qkhkp/VP5zfLEMQg1AE/YofkCIc/KSZOBpuroiQoCK0qTNkD4HzCzDa7ap5Q==
-----END PUBLIC KEY-----

privateB
-----BEGIN PRIVATE KEY-----
MIGcAgEAMFMGCSqGSIb3DQEDATBGAkEAiBB/FlC3W8aPLJxYGXzKsnpEmPKIKR4JetlA1ky+TKTYofXUKSFucGxtrmWlVFjnLZUqJFjj0bVDKSiYOfod1wIBAgRCAkBSsgvp3xivPK6Wp2X+SIjGllg1MT4zJdEoyUjV6iDLGytdeLpokYOO6xsGIiVb8b6A/5onnopra2iXBb0dS5rn
-----END PRIVATE KEY-----

dhparam
-----BEGIN DH PARAMETERS-----
MEYCQQCIEH8WULdbxo8snFgZfMqyekSY8ogpHgl62UDWTL5MpNih9dQpIW5wbG2uZaVUWOctlSokWOPRtUMpKJg5+h3XAgEC
-----END DH PARAMETERS-----

## Solution: 

We can use the Alice and Bob scenario to make sense to what we are given and decrypt the flag. We can use a Python script to do this. 

![Alice & Bob Diffie](https://upload.wikimedia.org/wikipedia/commons/c/c8/DiffieHellman.png)

We are given ``p`` (prime modulus), ``g`` (base), ``Alice's public key`` ($A_Y$), and ``Bob's private key`` ($B_X$). 

We can compute the shared secret using Python and the cryptography library:

```python
from cryptography.hazmat.primitives import serialization
from Crypto.Cipher import AES
import hashlib

alice_pub_key = b"""-----BEGIN PUBLIC KEY-----
MIGaMFMGCSqGSIb3DQEDATBGAkEAiBB/FlC3W8aPLJxYGXzKsnpEmPKIKR4JetlA1ky+TKTYofXUKSFucGxtrmWlVFjnLZUqJFjj0bVDKSiYOfod1wIBAgNDAAJAN3YrjXtIssyugO9tQ3BRy2TN92Qkhkp/VP5zfLEMQg1AE/YofkCIc/KSZOBpuroiQoCK0qTNkD4HzCzDa7ap5Q==
-----END PUBLIC KEY-----""" 

bob_private_key = b"""-----BEGIN PRIVATE KEY-----
MIGcAgEAMFMGCSqGSIb3DQEDATBGAkEAiBB/FlC3W8aPLJxYGXzKsnpEmPKIKR4JetlA1ky+TKTYofXUKSFucGxtrmWlVFjnLZUqJFjj0bVDKSiYOfod1wIBAgRCAkBSsgvp3xivPK6Wp2X+SIjGllg1MT4zJdEoyUjV6iDLGytdeLpokYOO6xsGIiVb8b6A/5onnopra2iXBb0dS5rn
-----END PRIVATE KEY-----"""

public_key = serialization.load_pem_public_key(alice_pub_key)
private_key = serialization.load_pem_private_key(
    bob_private_key, password=None)

shared_secret = private_key.exchange(public_key)
```

Once we have the shared secret, we can calculate the AES-256 key by hashing the value using SHA-256. 

```python
aes_key = hashlib.sha256(shared_secret).digest()
```

Now we have everything we need to load the encrypted file, decrypt it, and capture the flag.

```python
file = "flag.txt.enc"
with open(file, "rb") as f:
    enc_data = f.read()

iv = enc_data[:16]
flag = enc_data[16:]

cipher = AES.new(aes_key, AES.MODE_CBC, iv)
plaintext = cipher.decrypt(flag)

print(plaintext.decode('utf-8'))
```

Full code: 
```python
from cryptography.hazmat.primitives import serialization
from Crypto.Cipher import AES
import hashlib

alice_pub_key = b"""-----BEGIN PUBLIC KEY-----
MIGaMFMGCSqGSIb3DQEDATBGAkEAiBB/FlC3W8aPLJxYGXzKsnpEmPKIKR4JetlA1ky+TKTYofXUKSFucGxtrmWlVFjnLZUqJFjj0bVDKSiYOfod1wIBAgNDAAJAN3YrjXtIssyugO9tQ3BRy2TN92Qkhkp/VP5zfLEMQg1AE/YofkCIc/KSZOBpuroiQoCK0qTNkD4HzCzDa7ap5Q==
-----END PUBLIC KEY-----""" 


bob_private_key = b"""-----BEGIN PRIVATE KEY-----
MIGcAgEAMFMGCSqGSIb3DQEDATBGAkEAiBB/FlC3W8aPLJxYGXzKsnpEmPKIKR4JetlA1ky+TKTYofXUKSFucGxtrmWlVFjnLZUqJFjj0bVDKSiYOfod1wIBAgRCAkBSsgvp3xivPK6Wp2X+SIjGllg1MT4zJdEoyUjV6iDLGytdeLpokYOO6xsGIiVb8b6A/5onnopra2iXBb0dS5rn
-----END PRIVATE KEY-----"""


file = "flag.txt.enc"
with open(file, "rb") as f:
    enc_data = f.read()

iv = enc_data[:16]
flag = enc_data[16:]

public_key = serialization.load_pem_public_key(alice_pub_key)
private_key = serialization.load_pem_private_key(
    bob_private_key, password=None)

shared_secret = private_key.exchange(public_key)
aes_key = hashlib.sha256(shared_secret).digest()
cipher = AES.new(aes_key, AES.MODE_CBC, iv)
plaintext = cipher.decrypt(flag)


print(plaintext.decode('utf-8'))
```

The flag: ``poctf{uwsp_f1r3_4nd_br1m570n3}``