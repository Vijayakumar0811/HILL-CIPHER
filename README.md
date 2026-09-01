# HILL CIPHER
### NAME: VIJAYAKUMAR S
### REG NO: 212224040359

## EX. NO: 3 IMPLEMENTATION OF HILL CIPHER
 
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

```
#include <stdio.h>
#include <string.h>

int main()
{
    int key[3][3] = {
        {6, 24, 1},
        {13, 16, 10},
        {20, 17, 15}
    };

    int inv[3][3] = {
        {8, 5, 10},
        {21, 8, 21},
        {21, 12, 8}
    };

    char text[100], cipher[100], decrypt[100];
    int i, j, k, len;
    int sum;

    printf("Enter plaintext: ");
    scanf("%s", text);

    len = strlen(text);

    /* Add X for padding */
    while (len % 3 != 0)
    {
        text[len++] = 'X';
        text[len] = '\0';
    }

    /* Encryption */
    for (i = 0; i < len; i += 3)
    {
        for (j = 0; j < 3; j++)
        {
            sum = 0;

            for (k = 0; k < 3; k++)
                sum += key[j][k] * (text[i + k] - 'A');

            cipher[i + j] = (sum % 26) + 'A';
        }
    }

    cipher[len] = '\0';

    /* Decryption */
    for (i = 0; i < len; i += 3)
    {
        for (j = 0; j < 3; j++)
        {
            sum = 0;

            for (k = 0; k < 3; k++)
                sum += inv[j][k] * (cipher[i + k] - 'A');

            decrypt[i + j] = (sum % 26) + 'A';
        }
    }

    decrypt[len] = '\0';

    printf("\nEncrypted text : %s", cipher);
    printf("\nDecrypted text : %s\n", decrypt);

    return 0;
}

```
## OUTPUT

<img width="530" height="256" alt="image" src="https://github.com/user-attachments/assets/5dbc97f7-4795-477d-9fea-0f876f1b8c7a" />

## RESULT

Thus, the Hill Cipher is implemented Sucessfully.
