# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

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
#include <ctype.h>
#include <string.h>

int mod26(int x) {
    x %= 26;
    if (x < 0) x += 26;
    return x;
}

int main() {
    char keyStr[5], text[200], mode;
    int K[2][2], invK[2][2], det, detInv = -1;

    printf("Enter 4-letter UPPERCASE key: ");
    scanf("%4s", keyStr);

    printf("Encrypt or Decrypt? (E/D): ");
    scanf(" %c", &mode);

    printf("Enter UPPERCASE text: ");
    scanf("%199s", text);

    // convert text to uppercase
    for (int i = 0; text[i]; i++) text[i] = toupper(text[i]);

    // key matrix
    K[0][0] = keyStr[0] - 'A';
    K[0][1] = keyStr[1] - 'A';
    K[1][0] = keyStr[2] - 'A';
    K[1][1] = keyStr[3] - 'A';

    // determinant
    det = mod26(K[0][0] * K[1][1] - K[0][1] * K[1][0]);

    // find modular inverse of determinant
    for (int i = 0; i < 26; i++)
        if (mod26(det * i) == 1)
            detInv = i;

    if (detInv == -1) {
        printf("Key not invertible!\n");
        return 0;
    }

    // inverse matrix
    invK[0][0] = mod26(detInv *  K[1][1]);
    invK[0][1] = mod26(detInv * -K[0][1]);
    invK[1][0] = mod26(detInv * -K[1][0]);
    invK[1][1] = mod26(detInv *  K[0][0]);

    int n = strlen(text);
    if (n % 2 != 0) { text[n] = 'A'; text[n+1] = '\0'; n++; }

    char out[200];
    int a, b;

    for (int i = 0; i < n; i += 2) {
        a = text[i] - 'A';
        b = text[i+1] - 'A';

        int r1, r2;

        if (mode == 'E' || mode == 'e') {
            r1 = mod26(K[0][0] * a + K[0][1] * b);
            r2 = mod26(K[1][0] * a + K[1][1] * b);
        } else {
            r1 = mod26(invK[0][0] * a + invK[0][1] * b);
            r2 = mod26(invK[1][0] * a + invK[1][1] * b);
        }

        out[i] = r1 + 'A';
        out[i+1] = r2 + 'A';
    }

    out[n] = '\0';

    printf("Output: %s\n", out);
    return 0;
}


```
## OUTPUT
<img width="1821" height="552" alt="image" src="https://github.com/user-attachments/assets/532397a3-862e-4b7b-99d0-3fc7aa021585" />

<img width="1806" height="590" alt="image" src="https://github.com/user-attachments/assets/01adf517-44cc-4f43-980a-aac24024d5dd" />

## RESULT
Thus the python program to implement the hill cipher substitution techniques is completed and successfully executed

