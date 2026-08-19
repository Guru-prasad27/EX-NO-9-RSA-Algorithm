# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
#include <stdio.h>
#include <math.h>

// Function to find gcd
int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to find modular exponentiation (m^e mod n)
long long modExp(long long base, long long exp, long long mod) {
    long long result = 1;
    for (int i = 0; i < exp; i++)
        result = (result * base) % mod;
    return result;
}

int main() {
    int p, q, n, phi, e, d = 0;
    long long msg, c, m;

    printf("Enter two prime numbers (p and q): ");
    scanf("%d %d", &p, &q);

    n = p * q;
    phi = (p - 1) * (q - 1);

    // choose e
    for (e = 2; e < phi; e++) {
        if (gcd(e, phi) == 1)
            break;
    }

    // compute d
    for (int i = 1; i < phi; i++) {
        if ((i * e) % phi == 1) {
            d = i;
            break;
        }
    }

    printf("Public Key: {%d, %d}\n", e, n);
    printf("Private Key: {%d, %d}\n", d, n);

    printf("Enter message (number) to encrypt: ");
    scanf("%lld", &msg);

    c = modExp(msg, e, n);
    printf("Encrypted message: %lld\n", c);

    m = modExp(c, d, n);
    printf("Decrypted message: %lld\n", m);

    return 0;
}
```

## Output:

<img width="723" height="535" alt="image" src="https://github.com/user-attachments/assets/fc8b981f-9f5f-499e-9dcf-61ded5cbc5ef" />


## Result:
 The program is executed successfully.
