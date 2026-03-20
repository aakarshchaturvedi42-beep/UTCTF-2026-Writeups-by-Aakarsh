We are given:

1. A large prime p
2. A generator g
3. A value h = g^xmod p

   This is based on the Discrete Logarithm Problem, which is:
     Given g, h, and p, such that

                           g^x = h(mod p)
   We need to solve:
                   223^x = h(mod p)
   This is equivalent to finding:
                   x = log base g of h modulo p

   Step 1: Check Structure of 𝑝−1:
   We compute:
               p-1
   Then factor it.

   Step 2: Apply Pohlig–Hellman
   This algorithm works by:

1. Factoring p−1

2. Solving smaller discrete logs modulo each factor

3. Combining results using Chinese Remainder Theorem

Step 3: Solve Subproblems

For each factor qi:

        x mod qi
        
Step 4: Reconstruct 𝑥
Combine all modular solutions:
​


