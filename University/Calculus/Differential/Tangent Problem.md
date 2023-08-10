#finished

The tangent of a curve is a straight line that touches the curve in ONE point. It has the same direction as the curve in the contact point.

**Example 1: Find the equation of the tangent for $y = x^{2}$ in $P = (1,1)$.**

The slope $m$ is needed to find the equation, to calculate the slope (given two points in a line) we use $\frac{y_{2} - y_{1}}{x_{2} - x_{1}}$ but we only have one point.

We could come to an approximation for $m$ using another point over the curve $Q(x, x^{2}$) and calculate the slope $m_{PQ}$ using the line $PQ$

![[Pasted image 20230810084809.png]]


$$m_{PQ} = \frac{x^{2} - 1}{x - 1}$$
Using:
***$Q(1.5, 2.25)$
$x=1.5$

$$
\begin{aligned}
m_{PQ} &= \frac{2.25 - 1}{1.5 - 1} \\ \\
m_{PQ} &= 2.5
\end{aligned}
$$

If we put $Q$ closer to $P$, $x$ gets closer to $1$ (from right and left), we get a value for $m_{PQ}$ close to the real one $m$ in $(1, 1)$.

***From Right***

| x     | $m_{PQ}$ |
| ----- | -------- |
| 2     | 3        |
| 1.5   | 2.5      |
| 1.1   | 2.1      |
| 1.01  | 2.01     |
| 1.001 | 2.001    |


***From Left***

| x     | $m_{PQ}$ |
| ----- | -------- |
| 0     | 1        |
| 0.5   | 1.5      |
| 0.9   | 1.9      |
| 0.99  | 1.99     |
| 0.999 | 1.999    |

![[Pasted image 20230810101802.png]]

***Using Limits***
$$\lim_{x \to 1} \frac{x^{2}-1}{x-1}$$
$$\lim_{x \to 1} \frac{(x-1)(x+1)}{x-1}$$
$$\lim_{x \to 1} x+1 =2$$

***Slope-intercept form of tangent line in $P(1,1)$, $m = 2$***

$$
\begin{aligned}
y - y_{1} &= m(x - x_{1}) \\
y - 1 &= 2(x -1) \\
y &= 2x -1
\end{aligned}
$$


### Limit notation
 
$$\lim_{Q \to P} m_{PQ} = m$$