#in-progress 

An infinite sequence is a list of numbers $a_{1}, a_{2}, a_{3}, ..., a_{n}, ...$  in a given ORDER. 
Where $a_{1}, a_{2}, a_{3}, a_{n}$ are the terms (A.K.A members or elements).

Formally, a sequence is a function whose domain are the positive integers.

**Example 1: $2n$**

$$2, 4, 6, 8, ..., 2n, ...$$

The general behavior of the sequence can be defined as
$$a_{n} = 2n$$
## Narrow the domain to simplify things
If we have $a_{n} = 10 + 2n$ we get $12, 14, 16, 18$ 
This can be simplified if we pick another $n_{0}$ in which the sequence will start. Specifically, $n_{0} = 6$ and $b_{n} = 2n$

## Write by extension
You can write a sequence as $\{a_{n}\} = \{2, 4, 6, ..., 2n, ...\}$

## Cool Way
$\{a_{n}\} = \{2n\}_{n=1}^{\infty}$ 

## Visual Representation
![[Pasted image 20230808224944.png]]
## Limits and convergence
Sometimes, the terms of a sequence will approximate to a single value as $n$ increases.

**Example 2: Convergent Sequences**

1. $\{1, \frac{1}{2}, \frac{1}{3}, \frac{1}{4}, ..., \frac{1}{n}, ...\}$ will converge to 0
2. $\{0, \frac{1}{2}, \frac{2}{3}, \frac{3}{4}, \frac{4}{5}, ..., \frac{n}{n+1}, ...\}$ will converge to 1

**Example 3: Divergent Sequences**
1. $\{2, 4, 6, ..., 2n, ...\}$ will grow indefinitely as $n$ grows.
2. $\{1, -1, 1, -1, ..., (-1)^{n+1}, ...\}$ will always alternate between two values

### Using Limits
If $\lim_{n\to\infty} a_{n} = L$ then, $a_{n}$ will converge into $L$.

If $L$ does not exist, then the sequence diverges.

