## SECURE HASH FUNCTION (SHA)

## AIM:
Develop a program to implement Secure Hash Algorithm (SHA-1)
## SECURED HASH ALGORITHM-1 (SHA-1):
```
1. Append Padding Bits: This step is already implicitly handled by updating the message digest with the input string.

2. Append Length: Similarly, the length is implicitly taken care of when updating the message digest with the input string.

3. Prepare Processing Functions: Define a method processingFunction(t, B, C, D) that returns the appropriate function value based on the value of t.

4. Prepare Processing Constants: Define an array K containing the processing constant words.

5. Initialize Buffers: Initialize variables H0, H1, H2, H3, H4 with the initial values.

6. Processing Message in 512-bit blocks: Implement the pseudo-code in a loop that iterates over the blocks of the padded and appended message.
```
## PROGRAM
```
import hashlib

def sha1_hash(input_str):
    return hashlib.sha1(input_str.encode()).hexdigest()

def main():
    try:
        print("Message digest object info: ")
        print(" Algorithm = SHA1")
        print(" ToString = <SHA1 Object>")
        
        input_str = ""
        print()
        print(f"SHA1(\"{input_str}\") =", sha1_hash(input_str))
        
        input_str = "abc"
        print()
        print(f"SHA1(\"{input_str}\") =", sha1_hash(input_str))
        
        input_str = "abcdefghijklmnopqrstuvwxyz"
        print()
        print(f"SHA1(\"{input_str}\") =", sha1_hash(input_str))
        print("")
        
    except Exception as e:
        print("Exception:", e)

if __name__ == "__main__":
    main()

```
## OUTPUT:
![image](https://github.com/smriti1910/Ex-04_CNS/assets/133334803/b2ca2507-2d7a-4fba-a911-02bf01fda9ac)

## RESULT:
Thus SHA was implemented successfully.




  ## DIGITAL SIGNATURE STANDARD

## AIM:
To write a C program to implement the signature scheme named digital
signature standard (Euclidean Algorithm).
## ALGORITHM:
```
STEP-1: Alice and Bob are investigating a forgery case of x and y.
STEP-2: X had document signed by him but he says he did not sign that document digitally.
STEP-3: Alice reads the two prime numbers p and a.
STEP-4: He chooses a random co-primes alpha and beta and the x’s original signature x.
STEP-5: With these values, he applies it to the elliptic curve cryptographic equation to obtain
y
STEP-6: Comparing this ‘y’ with actual y’s document, Alice concludes that y is a
forgery.
```
## PROGRAM: (Digital Signature Standard)
```
import random
from sympy import mod_inverse, isprime, nextprime

class DSA:
    @staticmethod
    def get_next_prime(ans):
        test = int(ans)
        while not isprime(test):
            test += 1
        return test

    @staticmethod
    def find_q(n):
        start = 2
        while not isprime(n):
            while n % start != 0:
                start += 1
            n //= start
        return n

    @staticmethod
    def get_gen(p, q, r):
        h = random.randint(1, p - 1)
        return pow(h, (p - 1) // q, p)

    @staticmethod
    def generate_dsa():
        rand_obj = random.Random()
        p = DSA.get_next_prime("10600")
        q = DSA.find_q(p - 1)
        g = DSA.get_gen(p, q, rand_obj)

        print("p:", p, "\nq:", q, "\ng:", g)

        x = random.randint(1, q - 1)
        y = pow(g, x, p)
        
        k = 0
        hash_val = 0
        while k == 0 or hash_val == 0:
            k = random.randint(1, q - 1)
            hash_val = random.randint(1, p - 1)
        
        r = pow(g, k, p) % q
        k_inv = mod_inverse(k, q)
        s = (k_inv * (hash_val + x * r)) % q

        print("\nSecrets:")
        print("x:", x, "\nk:", k, "\ny:", y, "\nh:", hash_val)
        print("\nSignature:")
        print("r:", r, "\ns:", s)

        w = mod_inverse(s, q)
        u1 = (hash_val * w) % q
        u2 = (r * w) % q
        v = (pow(g, u1, p) * pow(y, u2, p)) % p % q

        print("\nVerification:")
        print("w:", w, "\nu1:", u1, "\nu2:", u2, "\nv:", v)

        if v == r:
            print("\nSuccess: Signature verified!")
        else:
            print("\nError: Incorrect signature")

if __name__ == "__main__":
    DSA.generate_dsa()

```
## OUTPUT:
![image](https://github.com/smriti1910/Ex-04_CNS/assets/133334803/d6294a22-8b35-4ce9-9934-829d24d69f33)


## RESULT:
Thus program to implement the signature scheme named digital signature standard (Euclidean Algorithm) is implementeds successfully.
