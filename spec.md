## circom-bigint spec
This page describes the circom-bigint circuit specifications, for examples, assumption on inputs and outputs, and the algorithm descriptions.

### What is bigint?
In circom, all operations are done in the field $\mathbb{F}_p$ where $p$ is a prime. By default, $\log(p) \approx 252.59$. Hence, all numbers are integers in the range $[0,p)$, called `signal`s. We need the capability to work with bigger numbers for things like Elliptic Curve cryptography.

A **bigint** number is represented as an array of $k$ field elements, each of which has $n$ bits. Basically, a $k$ digit number with base $2^n$.

### ModSum(n)
#### Specification
Input signals: $a, b$, both $n$-bit size with $n \leq 252$.

Output signals: $sum, carry$.

$sum$ is $(a+b) \% 2^n$.

$carry$ is a binary signal, 1 iff $(a+b) > 2^n$.

#### Description
Since $a$ and $b$ are assumed to be $n$-bit inputs, their addition can fit in $n$ bits, or in $n+1$ bits with the highest significant bit set to 1.

#### Notes for developers
$a$ and $b$ should be constrained to be $n$-bit wide by circuits inheriting this template.

### ModSub(n)
#### Specification
Input signals: $a, b$, both $n$-bit size with $n \leq 252$.

Output signals: $out, borrow$.

$out$ is $(a-b) \% 2^n$.

$borrow$ is a binary signal, 1 iff $a < b$.

#### Description
If $a \geq b$, subtraction in $\mod n$ is just $a-b$.

Otherwise, it is $2^n+a-b$. Since $a<b$, the $borrow$ bit is set to 1.

### ModSubThree(n)
#### Specification
Input signals: $a,b,c$, all $n$-bit size with $n+2 \leq 253$.

Output signals: $out, borrow, b_plus_c$.