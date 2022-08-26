## circom-bigint spec
This page describes the circom-bigint circuit specifications, for examples, assumption on inputs and outputs, and the algorithm descriptions.

### ModSum(n)
#### Specification
Input signals: $a, b$, both $n$-bit size.

Output signals: $sum, carry$.

$sum$ is $(a+b) \% 2^n$.

$carry$ is a binary signal, 1 iff $(a+b) > 2^n$.

### Description
Since $a$ and $b$ are assumed to be $n$-bit inputs, their addition can fit in $n$ bits, or in $n+1$ bits with the highest significant bit set to 1.

$a$ and $b$ should be constrained to be $n$-bit wide by circuits inheriting this template.
