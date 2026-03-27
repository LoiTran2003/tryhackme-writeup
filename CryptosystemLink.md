# tryhackme-writeup
TryHackMe – CryptosystemLinks Write‑Up
Author: loitran2003
Challenge: CryptosystemLinks
Write‑up URL: (https://github.com/LoiTran2003/tryhackme-writeup.git)

Overview
This challenge focuses on RSA vulnerabilities when the primes p and q are too close together. The provided code shows that q is generated as the next odd prime after p, making the modulus n easy to factor using a difference‑of‑squares attack.

Given Data
- RSA modulus n
- Public exponent e = 65537
- Ciphertext c
- Code showing how p and q were generated
Because q = next_prime(p), the primes differ by a very small value, making RSA insecure.

Attack Method
- Compute a = ceil(sqrt(n))
- Compute b² = a² − n
- If b² is a perfect square:
- p = a − b
- q = a + b
- Compute φ(n) = (p−1)(q−1)
- Compute private key d = inverse(e, φ(n))
- Decrypt using m = pow(c, d, n)
- Convert integer → bytes → UTF‑8 string

Recovered Flag
THM{Just_s0m3_small_amount_of_RSA!}

Conclusion
This challenge demonstrates why RSA requires strong randomness and sufficient separation between primes. Using next_prime(p) makes the modulus vulnerable to simple algebraic attacks.

