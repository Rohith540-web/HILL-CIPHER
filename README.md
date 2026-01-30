# HILL CIPHER

## EX. NO: 3 -IMPLEMENTATION OF HILL CIPHER

## AIM: 
To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```c
#include <stdio.h>
#include <string.h>

#define MOD 26

// Function to find modular inverse of determinant
int modInverse(int det) {
    det = det % MOD;
    for (int i = 1; i < MOD; i++) {
        if ((det * i) % MOD == 1)
            return i;
    }
    return -1;
}

int main() {
    char text[100];
    int key[2][2], invKey[2][2];
    int i, det, invDet;

    printf("Enter plaintext (EVEN length, uppercase): ");
    scanf("%s", text);

    int len = strlen(text);

    if (len % 2 != 0) {
        printf("Error: Text length must be even.\n");
        return 0;
    }

    printf("Enter 2x2 key matrix:\n");
    for (i = 0; i < 2; i++)
        for (int j = 0; j < 2; j++)
            scanf("%d", &key[i][j]);

    // Encryption
    printf("\nEncrypted Text: ");
    for (i = 0; i < len; i += 2) {
        int a = text[i] - 'A';
        int b = text[i + 1] - 'A';

        char c1 = (key[0][0]*a + key[0][1]*b) % MOD + 'A';
        char c2 = (key[1][0]*a + key[1][1]*b) % MOD + 'A';

        printf("%c%c", c1, c2);
    }

    // Determinant
    det = (key[0][0]*key[1][1] - key[0][1]*key[1][0]) % MOD;
    if (det < 0) det += MOD;

    invDet = modInverse(det);
    if (invDet == -1) {
        printf("\nKey matrix is not invertible.\n");
        return 0;
    }

    // Inverse key matrix
    invKey[0][0] = ( key[1][1] * invDet) % MOD;
    invKey[0][1] = (-key[0][1] * invDet) % MOD;
    invKey[1][0] = (-key[1][0] * invDet) % MOD;
    invKey[1][1] = ( key[0][0] * invDet) % MOD;

    for (i = 0; i < 2; i++)
        for (int j = 0; j < 2; j++)
            if (invKey[i][j] < 0)
                invKey[i][j] += MOD;

    // Decryption
    printf("\nDecrypted Text: ");
    for (i = 0; i < len; i += 2) {
        int a = text[i] - 'A';
        int b = text[i + 1] - 'A';

        char p1 = (invKey[0][0]*a + invKey[0][1]*b) % MOD + 'A';
        char p2 = (invKey[1][0]*a + invKey[1][1]*b) % MOD + 'A';

        printf("%c%c", p1, p2);
    }

    return 0;
}

```

## OUTPUT
<img width="810" height="452" alt="image" src="https://github.com/user-attachments/assets/a44800b2-8936-40a2-ac20-cfd4dfa12da7" />


## RESULT
Thus the implementation of HILL CIPHER had been executed successfully.  
