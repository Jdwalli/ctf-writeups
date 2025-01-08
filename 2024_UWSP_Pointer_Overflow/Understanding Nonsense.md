# Understanding Nonsense
Reverse, 100 points

## Description:
Oh, boy... Only Wave 2 and I'm already exhausted. Whatever the issue, I just can't be bothered to finish putting this challenge together. Here, this what I have so far. Started working on the decode function and gave up. You go ahead and do the rest and the flag is yours! And if Prof. Johnson asks, tell him this was really well done or I'll get in trouble.

## Solution:

Running the program gives us this result:

```shell
Encoded flag: Flag after reverse step 0: 8e79a99cacd5c5c7917aa58ab88dc6815583a5597bb987b851697b58bb8bcd
Decode function not added yet!Decoded flag (plaintext in hex): Flag after reverse step 0: 8e79a99cacd5c5c7917aa58ab88dc6815583a5597bb987b851697b58bb8bcd
```

The challenge additionally provides us with the source code:

```c
#include <stdio.h>
#include <string.h>

// Convert each byte of the flag to hex and print it
void print_flag_hex(unsigned char *flag, int length, int step) {
    printf("Flag after reverse step %d: ", step);
    for (int i = 0; i < length; i++) {
        printf("%02x", flag[i]);  // Print each byte in hexadecimal
    }
    printf("\n");
}

// Reverse the modification of the flag bytes based on the seed
void reverse_modify_flag(unsigned char *flag, unsigned int seed) {
    int length = strlen((char *)flag);

    for (int i = 0; i < length; i++) {
        flag[i] = (flag[i] - (seed % 10)) % 256;  // Reverse each byte modification
        seed = seed / 10;
        if (seed == 0) {
            seed = 88974713;  // Reset seed if it runs out
        }
    }
}

int main() {
    unsigned char encoded_flag[] = { 0x8e, 0x79, 0xa9, 0x9c, 0xac, 0xd5, 0xc5, 0xc7, 0x91, 0x7a, 0xa5, 0x8a, 0xb8, 0x8d, 0xc6, 0x81, 0x55, 0x83, 0xa5, 0x59, 0x7b, 0xb9, 0x87, 0xb8, 0x51, 0x69, 0x7b, 0x58, 0xbb, 0x8b, 0xcd};

    unsigned int seed = 88974713;
    int length = sizeof(encoded_flag);

    printf("Encoded flag: ");
    print_flag_hex(encoded_flag, length, 0);

    // Reverse the modifications 10 times (finish this!)
    printf("Decode function not added yet!");

    printf("Decoded flag (plaintext in hex): ");
    print_flag_hex(encoded_flag, length, 0);  // Print final decoded flag in hex

    return 0;
}
```

In order to solve this, we can modify the C code to use the `reverse_modify_flag` function ten times:

```c
#include <stdio.h>
#include <string.h>

// Convert each byte of the flag to hex and print it
void print_flag_hex(unsigned char *flag, int length, int step) {
    printf("Flag after reverse step %d: ", step);
    for (int i = 0; i < length; i++) {
        printf("%02x", flag[i]);  // Print each byte in hexadecimal
    }
    printf("\n");
}

// Reverse the modification of the flag bytes based on the seed
void reverse_modify_flag(unsigned char *flag, unsigned int seed) {
    int length = strlen((char *)flag);

    for (int i = 0; i < length; i++) {
        flag[i] = (flag[i] - (seed % 10)) % 256;  // Reverse each byte modification
        seed = seed / 10;
        if (seed == 0) {
            seed = 88974713;  // Reset seed if it runs out
        }
    }
}

int main() {
    unsigned char encoded_flag[] = { 0x8e, 0x79, 0xa9, 0x9c, 0xac, 0xd5, 0xc5, 0xc7, 0x91, 0x7a, 0xa5, 0x8a, 0xb8, 0x8d, 0xc6, 0x81, 0x55, 0x83, 0xa5, 0x59, 0x7b, 0xb9, 0x87, 0xb8, 0x51, 0x69, 0x7b, 0x58, 0xbb, 0x8b, 0xcd};

    unsigned int seed = 88974713;
    int length = sizeof(encoded_flag);

    printf("Encoded flag: ");
    print_flag_hex(encoded_flag, length, 0);

    // Reverse the modifications 10 times (finish this!)
    printf("Decode function not added yet!");
    int i = 0;
    while (i < 10) {
        reverse_modify_flag(encoded_flag, seed);
        i++;
    }

    printf("Decoded flag (plaintext in hex): ");
    print_flag_hex(encoded_flag, length, 0);  // Print final decoded flag in hex

    return 0;
}
```

Which will give the results hex encoded flag: `706f6374667b757773705f627233763137795f31355f3768335f353075317d`

Decoding this will give the flag.

The flag: `poctf{uwsp_br3v17y_15_7h3_50u1}`
