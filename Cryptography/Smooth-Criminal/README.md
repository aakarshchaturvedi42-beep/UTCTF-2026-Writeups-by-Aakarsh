## CTF Writeup: Discrete Logarithm Challenge

## Problem

We are given the following values:

- Prime modulus `p`
- Generator `g`
- Value `h = g^x mod p`

Goal: **Recover the secret exponent `x` and convert it into bytes to obtain the flag.**


---

## Understanding the Problem

We are given:

```

h = g^x mod p

```

This is a **Discrete Logarithm Problem (DLP)**:

> Find `x` such that:
>
> g^x ≡ h (mod p)

---

## Why Brute Force Fails

- `p` is ~1024 bits → extremely large
- Trying all possible values of `x` is computationally infeasible

---

## Approach

### Step 1: Identify the Problem Type

This is a **modular discrete logarithm problem**, commonly solved using:

- Baby-step Giant-step (BSGS)
- Pollard’s Rho
- Pohlig–Hellman (if `p-1` is smooth)

---

### Step 2: Analyze `p - 1`

We compute:

```

p - 1

```

If `p-1` factors into small primes, we can apply:

**Pohlig–Hellman Algorithm**

---

### Step 3: Apply Pohlig–Hellman

The algorithm works as follows:

1. Factor `p - 1`
2. Solve smaller discrete logs modulo each factor
3. Combine results using the Chinese Remainder Theorem (CRT)

---

### Step 4: Compute `x`

Instead of implementing from scratch, we can use existing libraries:

```python
from sympy.ntheory import discrete_log

x = discrete_log(p, h, g)

Step 5: Convert to Flag

Once x is found:
```
```python

from Crypto.Util.number import long_to_bytes
from sympy.ntheory import discrete_log

p = 1363402168895933073124331075716158793413739602475544713040662303260999503992311247861095036060712607168809958344896622485452229880797791800555191761456659256252204001928525518751268009081850267001
g = 223
h = 1009660566883490917987475170194560289062628664411983200474597006489640893063715494610197294704009188265361176318190659133132869144519884282668828418392494875096149757008157476595873791868761173517

x = discrete_log(p, h, g)
flag = long_to_bytes(x)

print("x =", x)
print("flag =", flag.decode())

x = 810642462826781236630409314742801724164468986543937060322593530182136957
flag = utflag{sm00th_cr1m1nal_caught}

```


The challenge is solvable because:

p - 1 is smooth (has small prime factors)
This allows efficient use of the Pohlig–Hellman algorithm


Conclusion:
The problem reduces to solving a discrete logarithm
Efficient algorithms make it tractable despite large numbers
The recovered exponent directly encodes the flag

​


