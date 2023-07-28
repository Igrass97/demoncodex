#in-progress 
In mathematics, a system of [[linear equations]] (or linear system) is a collection of one or more [[linear equations]] involving the same variables.

**Example 1: Linear equations system. m = 3, n = 3**
$$
\begin{aligned}
3x + 2y - z = 1 \\
2x -2y + 4z = -2 \\
-x + \frac{1}{2}y - z = 0
\end{aligned}
$$


A general system of m [[linear equations]] with n unknowns and coefficients can be written as

$$
\begin{aligned}
a_{11}x_1 + a_{12}x_2 + ... + a_{1n}x_{n} + b_1 = 0 \\
a_{21}x_1 + a_{22}x_2 + ... + a_{2n}x_{n} + b_2 = 0 \\
. \\
. \\
. \\
a_{m1}x_1 + a_{m2}x_2 + ... a_{mn}x_{n} + b_m = 0
\end{aligned}
$$
## Solution Set
A solution of a linear system is an assignment of values to the variables $x1, x2, ..., xn$ such that each of the equations is satisfied. The set of all possible solutions is called the solution set.

A linear system may behave in any one of three possible ways:

1. The system has _infinitely many solutions_.
2. The system has a single _unique solution_.
3. The system has _no solution_.

### Two Variables
Each equation represents a line in the xy plane, so the solution are the intersections:
1. The intersection is a line: $\infty$ solutions
2. The intersection is a point: 1 solution
3. No intersection: No solution

### Three Variables
Each linear equation determines a plane in three-dimensional space, and the solution set is the intersection of these planes.
1. If the intersection is a single point: 1 solution
2. If the intersection is a line: $\infty$ solutions
3. If the intersection is a plane: $\infty$ solutions
4. If they don't intersect: 0 solutions

### Ultimate Spell to Analyze System of [[Linear Equations]]

$$
\begin{aligned}
x + y = 3 \\
2x - 3y = 7 \\
3x + 2y = 4
\end{aligned}
$$

**Row Echelon Form**: is a specific form of a matrix where the leading coefficient (the leftmost nonzero entry) of each nonzero row is 1, and the leading 1 in each row is to the right of the leading 1 in the row above it. Additionally, all elements below the leading 1's are zeros. This form simplifies the process of solving systems of [[linear equations]] and makes it easier to identify the nature of the solutions.

**Example 2: Row Echelon Form**
$$
\begin{bmatrix}
1 & 2 & 3 & 4 \\
0 & 1 & 5 & 7 \\
0 & 0 & 1 & 2 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$


#### 1. Create the Augmented Matrix

$$
\begin{bmatrix}
1 & 1 & 3 \\
2 & -3 & 7 \\
3 & 2 & 4
\end{bmatrix}
$$
#### 2. Gaussian Elimination (Row Operations)
Now, we can use Gaussian elimination to transform the augmented matrix into row-echelon form.

Gaussian elimination is a systematic way to transform a matrix into row-echelon form using elementary row operations.

##### Elementary Operations
1. Multiply a row by a nonzero constant: This scales the entire row by a specific value.
2. Add a multiple of one row to another row: This allows you to eliminate a variable from one equation by adding it to another equation.
3. Swap two rows: This operation is used to change the order of rows in the matrix.

##### Steps
1. Start with the original augmented matrix representing the system of linear equations.
2. Choose a pivot element (the leading coefficient) in the first row. It's usually the leftmost nonzero entry in the first row.
3. Use row operations to make all elements below the pivot element zero.
4. Move to the second row and choose a pivot element. Perform row operations to make all elements below this pivot element zero.
5. Continue this process for the remaining rows, moving downward.
6. After reaching the last row or last column, the matrix should be in row-echelon form.
7. If necessary, perform back-substitution to find the solutions to the system of equations.

From the Augmented Matrix:
$$
$$
$$
\begin{bmatrix}
1 & 1 & 3 \\
2 & -3 & 7 \\
3 & 2 & 4
\end{bmatrix}
$$
1. Grab the pivot in R1 (1) and perform the following operations:
	**R2 = R2 - 2R1**
$$
\begin{bmatrix}
1 & 1 & 3 \\
0 & -5 & 1 \\
3 & 2 & 4
\end{bmatrix}
$$
	**R3 = R3 - 3R1**
$$
\begin{bmatrix}
1 & 1 & 3 \\
0 & -5 & 1 \\
0 & -1 & -5
\end{bmatrix}
$$
2. Grab the pivot in R2 (-5) and make all elements below 0
	**R3 = R3 + (-1/5 R2)**

$$
\begin{bmatrix}
1 & 1 & 3 \\
0 & -5 & 1 \\
0 & 0 & -\frac{26}{5}
\end{bmatrix}
$$