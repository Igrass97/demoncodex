#finished
**Big _O_ notation** is a mathematical notation that describes the limiting behavior of a function when the Argument tends towards a particular value or infinity.

In order to analyze and calculate an algorithm's performance, we must calculate and compare the worst-case runtime complexities of the algorithm. The order of O(1) - known as the Constant Running Time - is the fastest running time for an algorithm, with the time taken by the algorithm being equal for different input sizes. Although the Constant Running Time is the ideal runtime for an algorithm, it can be rarely achieved because the runtime depends on the size of n inputted.

It is an Asymptotic Notation for the worst case, which is also the ceiling of growth for a given function. It provides us with what is called an **_asymptotic upper bound_** for the growth rate of runtime of an algorithm or program.

f(n) is O(g(n)) if and only if f(n) <= C * g(n) for all n >= k,  
where C and k are positive constant values.

## Asymptotic analysis
Formally, given functions _f_ (_x_) and _g_(_x_), we define a binary relation
![[Pasted image 20230715215503.png]]
if and only if
![[Pasted image 20230715215530.png]]

The relation is an equivalence relation on the set of functions of x; the functions f and g are said to be asymptotically equivalent. The domain of f and g can be any set for which the limit is defined: e.g. real numbers, complex numbers, positive integers.
