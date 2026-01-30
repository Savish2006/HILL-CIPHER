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

## PROGRAM :
```PY
#include <stdio.h>
#include <string.h>

#define SIZE 3
#define MOD 26

int key[SIZE][SIZE];
int invKey[SIZE][SIZE];

int modInverse(int a)
{
    a = a % MOD;
    for (int x = 1; x < MOD; x++)
        if ((a * x) % MOD == 1)
            return x;
    return -1;
}

void getInverseKey()
{
    int det =
        key[0][0] * (key[1][1] * key[2][2] - key[1][2] * key[2][1]) -
        key[0][1] * (key[1][0] * key[2][2] - key[1][2] * key[2][0]) +
        key[0][2] * (key[1][0] * key[2][1] - key[1][1] * key[2][0]);

    det = (det % MOD + MOD) % MOD;
    int invDet = modInverse(det);

    invKey[0][0] = ( key[1][1]*key[2][2] - key[1][2]*key[2][1]) * invDet;
    invKey[0][1] = (-key[0][1]*key[2][2] + key[0][2]*key[2][1]) * invDet;
    invKey[0][2] = ( key[0][1]*key[1][2] - key[0][2]*key[1][1]) * invDet;

    invKey[1][0] = (-key[1][0]*key[2][2] + key[1][2]*key[2][0]) * invDet;
    invKey[1][1] = ( key[0][0]*key[2][2] - key[0][2]*key[2][0]) * invDet;
    invKey[1][2] = (-key[0][0]*key[1][2] + key[0][2]*key[1][0]) * invDet;

    invKey[2][0] = ( key[1][0]*key[2][1] - key[1][1]*key[2][0]) * invDet;
    invKey[2][1] = (-key[0][0]*key[2][1] + key[0][1]*key[2][0]) * invDet;
    invKey[2][2] = ( key[0][0]*key[1][1] - key[0][1]*key[1][0]) * invDet;

    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < SIZE; j++)
            invKey[i][j] = (invKey[i][j] % MOD + MOD) % MOD;
}

void process(char *text, int matrix[SIZE][SIZE], char *result)
{
    int len = strlen(text);
    int k = 0;

    for (int i = 0; i < len; i += 3)
    {
        for (int j = 0; j < SIZE; j++)
        {
            int sum = 0;
            for (int x = 0; x < SIZE; x++)
                sum += matrix[j][x] * (text[i + x] - 'A');

            result[k++] = (sum % MOD) + 'A';
        }
    }
    result[k] = '\0';
}

int main()
{
    char plain[100], encrypted[100], decrypted[100];

    printf("Enter Plain Text (UPPERCASE): ");
    scanf("%s", plain);

    if (strlen(plain) % 3 != 0)
        strcat(plain, "X");

    printf("Enter 3x3 Key Matrix:\n");
    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < SIZE; j++)
            scanf("%d", &key[i][j]);

    process(plain, key, encrypted);
    getInverseKey();
    process(encrypted, invKey, decrypted);

    printf("\nInput            : %s", plain);
    printf("\nEncrypted message: %s", encrypted);
    printf("\nDecrypted message: %s\n", decrypted);

    return 0;
}
```

## OUTPUT:




<img width="583" height="462" alt="image" src="https://github.com/user-attachments/assets/443031bd-daed-49d5-8450-444b09a10e5b" />




## RESULT:
The program is executed successfully
