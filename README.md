# EX-9-RSA ENCRYPTION ALGORITHM
## AIM:
To encrypt and decrypt a given message using the RSA (Rivest-Shamir-Adleman) algorithm.

## DESIGN STEPS:
### Step 1:
Design the RSA algorithm.

### Step 2:
Implement the RSA algorithm using C or Python.

### Step 3:
The RSA algorithm involves two keys: a public key for encryption and a private key for decryption. The keys are generated based on two large prime numbers. The encryption process uses the public key to convert plaintext into ciphertext, and decryption uses the private key to retrieve the original message.

## PROGRAM :
```c
#include <stdio.h>
#include <string.h>
#include <math.h>

// Function to calculate the greatest common divisor (GCD)
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to calculate (base^exp) % mod using modular exponentiation
int modExp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

// Function to find the modular inverse using the extended Euclidean algorithm
int modInverse(int a, int m) {
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;
    
    if (m == 1)
        return 0;

    while (a > 1) {
        q = a / m;
        t = m;
        m = a % m;
        a = t;
        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    if (x1 < 0)
        x1 += m0;

    return x1;
}

int main() {
    int p = 61, q = 53;  // Two large prime numbers
    int n = p * q;       // Calculate n
    int phi = (p - 1) * (q - 1);  // Calculate Euler's totient function
    int e = 17;          // Public key (e must be coprime with phi and 1 < e < phi)
    
    // Ensure that e is coprime with phi
    while (gcd(e, phi) != 1) {
        e++;
    }
    
    int d = modInverse(e, phi);  // Private key (d is the modular inverse of e mod phi)
    
    char plaintext[100];
    printf("Enter the plaintext: ");
    scanf("%s", plaintext);
    
    int encryptedMessage[100];
    int decryptedMessage[100];
    
    // Encrypt each character of the plaintext string
    printf("Encrypted Message: ");
    for (int i = 0; i < strlen(plaintext); i++) {
        encryptedMessage[i] = modExp(plaintext[i], e, n);
        printf("%d ", encryptedMessage[i]);
    }
    printf("\n");
    
    // Decrypt each character back to the original message
    printf("Decrypted Message: ");
    for (int i = 0; i < strlen(plaintext); i++) {
        decryptedMessage[i] = modExp(encryptedMessage[i], d, n);
        printf("%c", (char)decryptedMessage[i]);
    }
    printf("\n");
    
    return 0;
}
```
## OUTPUT:
![Screenshot 2024-10-10 095423](https://github.com/user-attachments/assets/ef7b429d-9b40-4c4b-8a16-6921e4008123)


## RESULT:
The RSA algorithm is implemented successfully.
