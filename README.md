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
#include <ctype.h>

int keymat[3][3] = {
    {1, 2, 1},
    {2, 3, 2},
    {2, 2, 1}
};

int invkeymat[3][3] = {
    {-1, 0, 1},
    {2, -1, 0},
    {-2, 2, -1}
};

char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

// Encode 3 characters
char *encode(char a, char b, char c)
{
    static char ret[4];
    int x, y, z;

    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];

    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';

    return ret;
}

// Decode 3 characters
char *decode(char a, char b, char c)
{
    static char ret[4];
    int x, y, z;

    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];

    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';

    return ret;
}

int main()
{
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;

    printf("Simulation of Hill Cipher\n");

    // Get input from user
    printf("Enter the message: ");
    fgets(msg, sizeof(msg), stdin);

    // Remove newline character
    msg[strcspn(msg, "\n")] = '\0';

    // Convert to uppercase and remove spaces
    int j = 0;
    for (int i = 0; msg[i] != '\0'; i++)
    {
        if (msg[i] != ' ')
        {
            msg[j++] = toupper(msg[i]);
        }
    }
    msg[j] = '\0';

    printf("Input message : %s\n", msg);

    // Padding with X
    n = strlen(msg) % 3;
    if (n != 0)
    {
        for (int i = 0; i < (3 - n); i++)
        {
            strcat(msg, "X");
        }
    }

    printf("Padded message : %s\n", msg);

    // Encryption
    for (int i = 0; i < strlen(msg); i += 3)
    {
        strcat(enc, encode(msg[i], msg[i + 1], msg[i + 2]));
    }

    printf("Encoded message : %s\n", enc);

    // Decryption
    for (int i = 0; i < strlen(enc); i += 3)
    {
        strcat(dec, decode(enc[i], enc[i + 1], enc[i + 2]));
    }

    printf("Decoded message : %s\n", dec);

    return 0;
}
```
## OUTPUT

<img width="722" height="312" alt="image" src="https://github.com/user-attachments/assets/8a9576da-877a-4e02-acaf-880814c52413" />

## RESULT

Thus, the Hill Cipher is implemented Sucessfully.
