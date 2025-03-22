# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MOD 26

// Function to find the determinant of a 2x2 matrix
int determinant(int key[2][2]) {
    return (key[0][0] * key[1][1] - key[0][1] * key[1][0]) % MOD;
}

// Function to find the modular inverse
int mod_inverse(int det, int mod) {
    det = (det % mod + mod) % mod;
    for (int i = 1; i < mod; i++) {
        if ((det * i) % mod == 1) {
            return i;
        }
    }
    return -1;
}

// Encrypt function
void encrypt(char *plaintext, int key[2][2]) {
    int len = strlen(plaintext);
    if (len % 2 != 0) {
        strcat(plaintext, "X"); // Padding if odd length
        len++;
    }
    
    printf("Ciphertext: ");
    for (int i = 0; i < len; i += 2) {
        int p1 = plaintext[i] - 'A';
        int p2 = plaintext[i + 1] - 'A';
        int c1 = (key[0][0] * p1 + key[0][1] * p2) % MOD;
        int c2 = (key[1][0] * p1 + key[1][1] * p2) % MOD;
        printf("%c%c", c1 + 'A', c2 + 'A');
    }
    printf("\n");
}

// Decrypt function
void decrypt(char *ciphertext, int key[2][2]) {
    int len = strlen(ciphertext);
    int det = determinant(key);
    int det_inv = mod_inverse(det, MOD);
    if (det_inv == -1) {
        printf("Key matrix is not invertible in mod 26.\n");
        return;
    }
    
    // Inverse key matrix
    int inverse_key[2][2];
    inverse_key[0][0] = key[1][1] * det_inv % MOD;
    inverse_key[0][1] = -key[0][1] * det_inv % MOD;
    inverse_key[1][0] = -key[1][0] * det_inv % MOD;
    inverse_key[1][1] = key[0][0] * det_inv % MOD;
    
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            if (inverse_key[i][j] < 0) inverse_key[i][j] += MOD;
        }
    }
    
    printf("Decrypted Text: ");
    for (int i = 0; i < len; i += 2) {
        int c1 = ciphertext[i] - 'A';
        int c2 = ciphertext[i + 1] - 'A';
        int p1 = (inverse_key[0][0] * c1 + inverse_key[0][1] * c2) % MOD;
        int p2 = (inverse_key[1][0] * c1 + inverse_key[1][1] * c2) % MOD;
        printf("%c%c", p1 + 'A', p2 + 'A');
    }
    printf("\n");
}

int main() {
    int key[2][2] = {{6, 24}, {1, 13}}; // 2x2 Key Matrix
    char plaintext[100] = "HELP";
    char ciphertext[100];
    
    printf("Plaintext: %s\n", plaintext);
    encrypt(plaintext, key);
    
    strcpy(ciphertext, "ZEBB"); // Output from encryption step
    decrypt(ciphertext, key);
    
    return 0;
}
```


## OUTPUT:

![exp 1c](https://github.com/user-attachments/assets/9de441c7-c4da-4edb-89fd-459ca35b09db)


## RESULT:
The program is executed successfully



